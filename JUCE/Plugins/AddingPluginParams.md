# Adding Plugin Parameters

In this tutorial we will be analyzing the gain demo project provided to us by [JUCE](https://docs.juce.com/master/tutorial_audio_parameter.html). The following tutorial will also be found in the resource section below.

## The Gain Processor

### Configuring the parameters

The audio processor is where all your audio parameter members should be stored. In this case we just have the `gain` parameter which is a `AudioParameterFloat` object.

```
private:
   //==============================================================================
   juce::AudioParameterFloat* gain;


   //==============================================================================
   JUCE_DECLARE_NON_COPYABLE_WITH_LEAK_DETECTOR (TutorialProcessor)
```

The next step is two add the parameter into the processor's constructor. Below we use the `addParameter` method from the `AudioProcessor` class so the processor can manage and delete the `gain` parameter whenever needed.

```
TutorialProcessor()
{
   addParameter (gain = new juce::AudioParameterFloat ("gain", // parameterID
                                                       "Gain", // parameter name
                                                       0.0f,   // minimum value
                                                       1.0f,   // maximum value
                                                       0.5f)); // default value
}
```

The `AudioParameterFloat` constructor takes 5 arguments named accordingly above. Note that the parameterID has to be a unique identifier and is treated as if naming a variable (no spaces and so on). The parameter name is what is displayed to the end user.

The minimum, maximum, and default values are self explanatory, but there is an alternative shorthand way of writing the minimum and maximum arguments. The ` NormalisableRange<float>` object is able to set a range of values. Here is an example of a declaration that does the same thing but with `NormalisableRange<float>`.

```
addParameter (gain = new juce::AudioParameterFloat ("gain",                                      // parameter ID
                                                   "Gain",                                      // parameter name
                                                   juce::NormalisableRange<float> (0.0f, 1.0f), // parameter range
                                                   0.5f));  //default value
```

## Performing the gain processing

Once our parameter is initialized in the processor, we can access this parameter in our `processBlock` method.

```
void processBlock (juce::AudioSampleBuffer& buffer, juce::MidiBuffer&) override
{
   buffer.applyGain (*gain);
}
```

The AudioSampleBuffer::applyGain() function applies our gain value to all samples across all channels in the buffer.

Dereferencing the pointer `gain` will give us the parameter value, in this case a float value. Using the template, `AudioParameterXXX`, you can replace the `XXX` with any data type you want that parameter to return.

## Storing and retrieving parameters

The `getStateInformation` method from the `AudioProcessor` class is a callback function when the plug-in needs to have its state stored.

```
void getStateInformation (juce::MemoryBlock& destData) override
{
   juce::MemoryOutputStream (destData, true).writeFloat (*gain);
}
```

In this example, we write a floating point value, gain, in a binary format into the `MemoryBlock` object. The `MemoryOutputStream` takes two arguments. One being the memory block addressed and the other a boolean denoting whether or not to append to the existing block content (the memory block in this case).

The `setStateInformation` method from the `AudioProcessor` class does the opposite in that it reads from a memory location and restores that state to the plug-in.

```
void setStateInformation (const void* data, int sizeInBytes) override
{
   *gain = juce::MemoryInputStream (data, static_cast<size_t> (sizeInBytes), false).readFloat();
}
```

The `setStateInformation` passes two arguments: `data` being the source data and `sizeInBytes` of that source data. Once the source data is read from the `MemoryInputStream` method, it is assigned to the `gain` variable.

## Improving the gain processor

Two ways to improve our gain processor:

- Changing gain causes discontinuities in the signal and this can be heard as little clicks if the gain is modulated quickly.
- Storing the plug-in's state is more convenient using XML.

### Smoothing gain changes

To smooth the gain changes, we can ramp through the entire buffer. To do this we store the gain value from the previous audio callback. First we declare a floating point variable called `previousGain`.

```
private:
   //==============================================================================
   juce::AudioParameterFloat* gain;
   float previousGain;


   //==============================================================================
   JUCE_DECLARE_NON_COPYABLE_WITH_LEAK_DETECTOR (TutorialProcessor)
```

We ensure that `previousGain` is initialized by using the `prepareToPlay` method from the `AudioProcessor` class. The `prepareToPlay` method is called before playback has started to prepare the processor.

```
void prepareToPlay (double, int) override
{
   previousGain = *gain;
}
```

Finally, we add a gain ramp to our `processBlock` method whenever the previous gain is not approximately equal to our current gain value. This fades the range between `previousGain` to `currentGain` creating a smoother transition between the two values.

### Using XML to store state

Storing state either as an XML or JSON is easier for debugging JUCE projects in the future. In this tutorial we will store our data in an XML format.

First step is to store our gain parameter in `getStateInformation`.

```
void getStateInformation (juce::MemoryBlock& destData) override
{
   std::unique_ptr<juce::XmlElement> xml (new juce::XmlElement ("ParamTutorial"));
   xml->setAttribute ("gain", (double) *gain);
   copyXmlToBinary (*xml, destData);
}
```

In this example, we create a smart pointer variable called `xml` which stores a new JUCE XML element called `ParamTutorial`. We then call the `setAttribute` method and pass the attributes name and value. Lastly, we then convert the xml to a binary block given while also passing `destData` as the size in bytes.

Next, we read our state of our gain using the `setStateInformation` method.

```
void setStateInformation (const void* data, int sizeInBytes) override
{
   std::unique_ptr<juce::XmlElement> xmlState (getXmlFromBinary (data, sizeInBytes));


   if (xmlState.get() != nullptr)
       if (xmlState->hasTagName ("ParamTutorial"))
           *gain = (float) xmlState->getDoubleAttribute ("gain", 1.0);
}
```

Here, we do a similar step as our `getStateInformation` method in creating a variable `xmlState` that contains the XML state from `data` and `sizeInBytes`. Then we have two nested conditions: one to check if the pointer is not null and the other to check if the state has the same tagname to our parameter `gain`. If both conditions are true, we then finally read the `xmlState` variable using `getDoubleAttribute` and assign its value to `gain`. The `getDoubleAttribute` takes two arguments: the attribute name and the default return value if the attribute name doesn't exist.

## Adding a phase invert parameter

In order to swap the phase of our audio, first make a boolean parameter with the `AudioParameterBool` object.

```
private:
   //==============================================================================
   juce::AudioParameterFloat* gain;
   juce::AudioParameterBool* invertPhase;


   float previousGain;


   //==============================================================================
   JUCE_DECLARE_NON_COPYABLE_WITH_LEAK_DETECTOR (TutorialProcessor)
```

Next, we add this parameter into our processor's constructor.

```
   TutorialProcessor()
   {
       addParameter (gain        = new juce::AudioParameterFloat ("gain", "Gain", 0.0f, 1.0f, 0.5f));
       addParameter (invertPhase = new juce::AudioParameterBool  ("invertPhase", "Invert Phase", false));
   }
```

Now we can update and retrieve our `invertPhase` state using the `getInformationState` and `setInformationState` methods.

```
void getStateInformation (juce::MemoryBlock& destData) override
{
   std::unique_ptr<juce::XmlElement> xml (new juce::XmlElement ("ParamTutorial"));
   xml->setAttribute ("gain", (double) *gain);
   xml->setAttribute ("invertPhase", *invertPhase); // [4]
   copyXmlToBinary (*xml, destData);
}


void setStateInformation (const void* data, int sizeInBytes) override
{
   std::unique_ptr<juce::XmlElement> xmlState (getXmlFromBinary (data, sizeInBytes));


   if (xmlState.get() != nullptr)
   {
       if (xmlState->hasTagName ("ParamTutorial"))
       {
           *gain = (float) xmlState->getDoubleAttribute ("gain", 1.0);
           *invertPhase = xmlState->getBoolAttribute ("invertPhase", false);
       }
   }
}
```

Then we head to our `processBlock` method to change the phase depending on the boolean value of`invertPhase`.

```
void processBlock (juce::AudioSampleBuffer& buffer, juce::MidiBuffer&) override
{
   auto phase = *invertPhase ? -1.0f : 1.0f;  // [6]
   auto currentGain = *gain * phase;          // [7]


   if (juce::approximatelyEqual (currentGain, previousGain))
   {
       buffer.applyGain (currentGain);
   }
   else
   {
       buffer.applyGainRamp (0, buffer.getNumSamples(), previousGain, currentGain);
       previousGain = currentGain;
   }
}
```

Lastly, we update our `previousGain` variable in the `prepareToPlay` method.

```
void prepareToPlay (double, int) override
{
   auto phase = *invertPhase ? -1.0f : 1.0f;
   previousGain = *gain * phase;
}
```
