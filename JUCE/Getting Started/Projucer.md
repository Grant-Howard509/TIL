# Getting Started with Projucer

When launching the projucer, you will see the `new project` window. On the left side, you will see the project type selection. For each type of project, projucer will provide the minimum code needed to get started for that project.

When creating a project you will:

- Name your project
- Specify which modules to include (or exclude) in the project
- Export the project to specified IDE's

Once these specifications are in, click `Create Project` to generate the project in a location of your choice.

To open existing projects, you can either click on the `.jucer` file in your project directory or `Open Existing Project` in the projucer application.

## Managing your Pojucer Projects

When creating a JUCE project, there are three subfolders that are created:

- Source
- Builds
- JuceLibraryCode

The source folder contains the main C++ code for the JUCE app. The builds folder contains the project on the IDE exports such as Xcode and Visual Studio. Lastly, we have the JuceLibarayCode which contains header files to the JUCE library code via modules.

### Adding and Editing Source Files

Projucer provides its own basic code editor that can be pulled up anytime in the `File explorer`. Here you can add, rename, and delete source files from your project.

NOTE: Do not add, remove, or delete from your native IDE project. Changes will be overwritten once the project is saved in Projucer.

### JUCE Modules

Some JUCE modules are dependent on other modules in order to function. We can see if a module is broken if it is highlighted red. If a module is broken, we can either add the dependency module, or delete the broken module in teh module settings.

The module settings menu also allows you to set their paths. Also, you can set global paths to modules by enabling it in the module settings menu as well.

Clicking on an individual module will provide module specific settings and properties.

### Export Targets and Build Settings

The `Exporter` tab allows us to see all builds and their settings. This is the place to specify additional compiler and linker flags and other platform-specific build settings.

You can also add additional builds to export the project to as well as delete current builds from this menu.
