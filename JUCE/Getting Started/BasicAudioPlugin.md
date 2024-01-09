JS/Promises.md# Basic Audio Plugin

First we need to create our project. To do so, open the projucer and select `Basic Plugin` from the project type menu. Once a project type is selected, name your project and click `Create Project`.

We will be making a VST3 plugin, to configure your project to target a VST3 plugin build, go into settings and find `Plugin Formats`. When you find `Plugin Formats` select VST3.

We will also be including MIDI as input and output for our project so again in our project settings find `Plugin Characteristics` and select `Plugin MIDI Output` and `Plugin MIDI Input`.

## Orientation

There are two main classes in our project: `PluginProcessor` (AudioProcessor) and `PluginEditor` (AudioProcessorEditor).

The `PluginProcessor` handles all MIDI IO and audio processing logic while `PluginEditor` handles the graphical controls and UI. It is best to think of `PluginProcessor` as the parent to `PluginEditor`.

There is only one processor where you can have multiple editors Each editor has a reference to the processor such that it can edit or access information and parameters from the audio thread. It is the editor’s job to set and get information on this processor thread and not the other way around.

In the `PluginProcessor` class we have a method called `processBlock()`. It is the main method that receives and produces audio and MIDI data. The main method we will use in the `PluginEditor` is its constructor to set our graphical user interface and all its parameters. The `paint()` method is also quite often used to draw controls and custom GUI components.

In the `PluginEditor` constructor, we have a method `setSize(400, 300)` which sets the width and height to 400 and 300 pixels respectively. In this example we set the plugin window to 200 x 200 pixels.

```
BasicPluginAudioProcessorEditor::BasicPluginAudioProcessorEditor (BasicPluginAudioProcessor& p)
   : AudioProcessorEditor (&p), audioProcessor (p)
{
   setSize (200, 200);
}
```

## Create a Simple GUI Control

In this tutorial we will create a basic slider from the `juce_gui_basics` module. First we need to create a new slider called `midiVolume`in the `PluginEditor` header file.

```
class BasicPluginAudioProcessorEditor  : public juce::AudioProcessorEditor
{
public:
   BasicPluginAudioProcessorEditor (BasicPluginAudioProcessor&);
   ~BasicPluginAudioProcessorEditor() override;


   //==============================================================================
   void paint (juce::Graphics&) override;
   void resized() override;


private:
   BasicPluginAudioProcessor& audioProcessor;


   juce::Slider midiVolume; // SLIDER HERE


   JUCE_DECLARE_NON_COPYABLE_WITH_LEAK_DETECTOR (BasicPluginAudioProcessorEditor)
};
```

With `midiVolume` defined in our header file, we can add the slider with all its properties in our editor constructor. Be sure to call addAndMakeVisible(&midiVolume) in the constructor to make the slider visible.

```
BasicPluginAudioProcessorEditor::BasicPluginAudioProcessorEditor (BasicPluginAudioProcessor& p)
   : AudioProcessorEditor (&p), audioProcessor (p)
{
   setSize (200, 200);


   midiVolume.setSliderStyle(juce::Slider::LinearBarVertical);
   midiVolume.setRange(0.0, 127.0, 1.0);
   midiVolume.setTextBoxStyle(juce::Slider::NoTextBox, false, 90, 0);
   midiVolume.setPopupDisplayEnabled (true, false, this);
   midiVolume.setTextValueSuffix (" Volume");
   midiVolume.setValue(1.0);


   addAndMakeVisible (&midiVolume);
}
```

Once we have all of our properties for our slider, we must set the size and position relative to the window inside the `resized()` method in our editor.

```
void BasicPluginAudioProcessorEditor::resized()
{
   midiVolume.setBounds (40, 30, 20, getHeight() - 60);
}
```

Finally, we add custom GUI components inside of the `paint()` method to complete our gui styling

```
void BasicPluginAudioProcessorEditor::paint (juce::Graphics& g)
{
   // fill the whole window white
      g.fillAll (juce::Colours::white);


      // set the current drawing colour to black
      g.setColour (juce::Colours::black);


      // set the font size and draw text to the screen
      g.setFont (15.0f);


      g.drawFittedText ("Midi Volume", 0, 0, getWidth(), 30, juce::Justification::centred, 1);
}
```

## Passing Control Information to Our Processor

In order to get the value from our slider to the processor, we need to create a new variable in our processor header file.

```
public:
   float noteOnVel;
```

Next, we make a slider listener callback function that will detect any changes to our slider component.

```
class BasicPluginAudioProcessorEditor  : public juce::AudioProcessorEditor,
                                        private juce::Slider::Listener // Inherited Slider Listener
{
public:
   BasicPluginAudioProcessorEditor (BasicPluginAudioProcessor&);
   ~BasicPluginAudioProcessorEditor() override;


   //==============================================================================
   void paint (juce::Graphics&) override;
   void resized() override;


private:
   void sliderValueHasChanged (juce::Slider* slider) override; // Slider Callback Function


   // This reference is provided as a quick way for your editor to
   // access the processor object that created it.
   BasicPluginAudioProcessor& audioProcessor;


   juce::Slider midiVolume; // SLIDER HERE


   JUCE_DECLARE_NON_COPYABLE_WITH_LEAK_DETECTOR (BasicPluginAudioProcessorEditor)
};
```

Then we add the listener to the editor's constructor.

```
BasicPluginAudioProcessorEditor::BasicPluginAudioProcessorEditor (BasicPluginAudioProcessor& p)
   : AudioProcessorEditor (&p), audioProcessor (p)
{
   // Make sure that before the constructor has finished, you've set the
   // editor's size to whatever you need it to be.
   setSize (500, 500);


   midiVolume.setSliderStyle(juce::Slider::LinearBarVertical);
   midiVolume.setRange(0.0, 127.0, 1.0);
   midiVolume.setTextBoxStyle(juce::Slider::NoTextBox, false, 90, 0);
   midiVolume.setPopupDisplayEnabled (true, false, this);
   midiVolume.setTextValueSuffix (" Volume");
   midiVolume.setValue(1.0);


   // add listener
   midiVolume.addListener (this);


   addAndMakeVisible (&midiVolume);
}
```

And then insert the listener function that set our public processor volume variable `noteOnVel`.

```
void BasicPluginAudioProcessorEditor::sliderValueChanged (juce::Slider* slider)  {
   audioProcessor.noteOnVel = midiVolume.getValue();
}
```

## MIDI/Audio signal

As mentioned previously, the process block receives and produces midi/audio buffers in real time. Here, we are going to iterate over the Midi buffer and change its velocity according to our slider's velocity from its `noteOn` type.

```
void BasicPluginAudioProcessor::processBlock (juce::AudioBuffer<float>& buffer, juce::MidiBuffer& midiMessages)
{
   buffer.clear();


   juce::MidiBuffer processedMidi;


   for (const auto metadata : midiMessages)
   {
       auto message = metadata.getMessage();
       const auto time = metadata.samplePosition;


       if (message.isNoteOn())
       {
           message = juce::MidiMessage::noteOn (message.getChannel(),
                                                message.getNoteNumber(),
                                                (juce::uint8) noteOnVel);
       }


       processedMidi.addEvent (message, time);
   }


   midiMessages.swapWith (processedMidi);
}
```

Let's break down this code. First, we clear our audio buffer named `buffer`. This will set all the samples to zero since audio samples are not important in this particular tutorial. Next we create a new `MidiBuffer` object called `processedMidi`. Although there may already be a `MidiBuffer` called `midiMessages`, we differentiate between the processed and unprocessed signals and swap the two signals when needed to avoid direct modification errors.

The first loop then loops over all the messages, called `metadata`, in the original `MidiBuffer` object `midiMessages`. Then we get the midi message from the midi buffer and assign it to `message` and assign the message's timestamp to `time`. Next we check if the midi key-down event is on, if true we create a key-down message and assign it to `message`. The `noteOn` method takes in the given channel, the note number, and the notes velocity.

In the last steps of the code, we create an event to the `processedMidi` object, then swap our processed buffer with the original `midiMessages` object.
