## Welcome to the ImprovOid GitHub

This repository currently contains some Audio Applications that are Open Source.

## Submission to the KVR Developer Challenge 2021 Contest - EchoMatrix VST3 for Windows (also MacOS VST3 and AU)

This project will be submitted to the KVR Developer Challenge 2021 contest to highlight the power of the Faust DSP development environment and the JUCE framework to create a non-trivial effect VST3 using a managable amount of Faust DSP code.

The download links are disabled until the contest begins ...

[Github source is here](https://github.com/improvoid/EchoMatrix)
You'll want to look at EchoMatrix.dsp. It is the Complete source code, the C++ is generated from it!

[Download the installer from GitHub](https://github.com/improvoid/EchoMatrix/blob/main/EchoMatrix/Install/EchoMatrixSetup.exe)

<a id="raw-url" href="https://github.com/improvoid/EchoMatrix/raw/main/EchoMatrix/Install/EchoMatrixSetup.exe">Maybe Quicker Installer Download</a>

When you run the installer, you will probably need to select "More" and "Run Anyway" as this is not recognized as an "official" installer.

You can also just download the Windows version of echomatrix.vst3 and put it where you want.

[Echomatrix VST3](github.com/improvoid/EchoMatrix/raw/main/EchoMatrix/Install/Win10/echomatrix.vst3)

I have also discovered that a number of Win 10 PCs may need to install the VC redistributable to get the VST3 to work. I did update the installer, but if it does not work for you, here are a couple of links to get the VC redistributable.

[Microsoft Support Page](support.microsoft.com/en-us/topic/the-latest-supported-visual-c-downloads-2647da03-1eea-4433-9aff-95f26a218cc0)

[Download Link for vc_redistx64.exe](aka.ms/vs/16/release/vc_redist.x64.exe)

MacOS Install Pkg (I am not a MacOS expert, I tested this and it seems to work):
 * Installs VST3 to \Library\Audio\Plug-Ins\VST3.
 * Installs AU to \Library\Audio\Plug-Ins\Components.

[EchoMatrixMacOS Package](https://github.com/improvoid/EchoMatrix/raw/main/EchoMatrix/Install/MacOS/EchoMatrixMacOS.pkg)

If you can't get the Pkg to work there is a Zip with the VST3 and AU that would need to manually be put in the correct directories.

[EchomatrixMacOS Zip](https://github.com/improvoid/EchoMatrix/raw/main/EchoMatrix/Install/MacOS/EchoMatrixMacOS.zip)

There is also a .dmg (drive image) with both of the files in it. Just copy to the correct location.

[A MacOS Drive Image (dmg)](https://github.com/improvoid/EchoMatrix/raw/main/EchoMatrix/Install/MacOS/EchoMatrixPkg.dmg)


## Faust and EchoMatrix

Faust is a powerful functional/mathematical language that can be a little difficult to learn but can create very complex DSP functions.
DSP effect and synthesizer projects can be created rapidly with a minimum amount of code.

One of the great things about Faust, is that you can code a complex DSP function with a small amount of code and modify it to do additional functions easily. These functions can be tested online using either the Faust online editor or the Faust IDE.

There is a great Kadenze course on Faust where some of the original designers and coders of Faust are teaching the course. Without this course, it is unlikely that I would have been able to code EchoMatrix. There is also some courses on JUCE that are good as well, but not really needed to get the basic functionality for EchoMatrix.

Faust can "export" DSP to many different platforms (even IOT devices).  In the case of the EchoMatrix, the Faust DSP code was exported to the JUCE C++ audio VST framework.

The EchoMatrix project is an example of a non-trivial implementation of a Faust DSP algorithm that should provide a good starting point for many possible variations.  I encourage anyone to use and enhance and re-use any part this code. 

## EchoMatrix Quick Description

The EchoMatrix was designed to provide some of the functionality of the Yamaha UD Stomp pedal as used be Alan Holdsworth. The UD Stomp pedal is composed of 8 delays that have a tap and can be modulated and configured to feed into one another to make "longer" delay lines. In the case of Alan Holdsworth, he would use a number of short delays, sometimes slightly modulated, and panned in the stereo sound field to make a very "fat" sound. The EchoMatrix has most of this functionality in a different package. The version of EchoMatrix as submitted only has 6 delays, but can be expanded to 8 delays by changing one line in the source code.  The only issue with adding more delays, is that it adds more controls to the feedback matrix.

EchoMatrix is a VST3 effect that provides a 6 delays that can be modulated and are connected by a feedback "echo" matrix.  

A "complete" input, feedback, and output mixer matrix of 6 delays and 2 channel input and output are provided so that:
	Inputs can be assigned to any delay at any volume.
	Delay output can be sent to any delay input (introducing extra delay or feedback).
	Delay output can be sent to either output channel at any volume, (so it can pan anywhere in the stereo field).

Delay controls are provided so that:
	Delays can be assigned a delay time.
	Delays can be modulated by a morphing wave shape with a variable frequency and modulation amount.

This allows flexibility in creating any feedback pattern that you can dream of.

The delays are controlled by "exponential" delay time controls that allows for more short delay time accuracy (by the knobs), but a desired delay can be typed into the input box below the knob. 
 
The UI is entirely defined in the Faust code, and as such is defined by a limited number of options. That is why the "multiple" controls are all defined with numbers starting with 0 (Unit 0, Delay 0 ... in the case of EchoMatrix). This could be modified to be more friendly using manual coding in the JUCE source code, but for now the UI defined by Faust is OK and allows for prototyping other functions for the EchoMatrix easily.

## EchoMatrix UI and Operation 

The EchomMatrix UI at first is a little confusing, but it is "mathematically" consistent because of Faust.

The interface has two "tabs", one to control the Delay parameters and one for the MatrixMixer.

The Delays tab contains four controls for each of the delays as shown in the image below:
 * Delay Time: DT U0 to U5
 * ModFreq (Modulation Frequency): MF U0 to U5
 * ModWave (Modulation Wave from Saw to Sin To Rev Saw): MW U0 to U5
 * ModDepth (Modulation Depth): MD U0 to U5
	
![DelaysTab](https://github.com/improvoid/EchoMatrix/raw/main/Images/VST_Delays_Tab.png)
	
In the Matrix Mixer for 6 delay channels:
 * There is an 8 x 8 Matrix Mixer.
 * Each of the first 6 rows, row 1 to row 6 (Unit-0 to Unit-5), are the inputs to each of the 6 delay lines.
 * The last 2 rows, row 7 and row 8 (Unit-6 and Unit-7), are the "input" to the "Left Audio Output" and the "Right Audio Output".
 * Each of the first 6 Columns, column 1 to column 6 (Unit-0 to Unit-5), are the outputs from each of the 6 delay lines.
 * The last 2 columns, column 7 and column 8 (Unit-6 and Unit-7), are the "output" from the "Left Audio Input" and the "Right Audio Input".

![MatrixMixerTab](https://github.com/improvoid/EchoMatrix/raw/main/Images/VST_MatrixMixer_Tab.png)

To make the numbers more consistent in the following description, lets number the delays from 0 to 5;
* So the 1st delay is called Delay 0 or Unit 0 and the 6th delay is Delay 5 or Unit 5.
* The "Left Audio Channel" corresponds to Unit 6 and the "Right Audio Channel" corresponds to Unit 7.

This means that to "connect" the Left Audio Input (Unit 6) to the input of Delay 0 (Unit 0), the knob in the column 7 and row 1 needs to be turned up.
* The amount that it is turned up determines the amount of the "Left Audio Input" that will be fed into Delay 0.
* To send the output from Delay 0 to the "Left Audio Output", the knob in the column 1 and the row 7 needs to be turned up.
* The amount of signal output from Delay 0 to the Left Audio Output is controlled by the knob.

To provide feedback in Delay 0 (Unit 0), turn up the knob in the Matrix Mixed row 1 and column 1.
* This will feed the output of Delay 0 (Unit 0) into the input of Delay 0 (Unit 0).

To mix some of the non-delayed "Left Audio Input" (Unit 6) into the "Left Audio Output" (Unit 6) the knob in column 7 and row 7 must be turned up. 

To get the delay effect to work as expected, the Delay tab needs to be used:
* Change the length of the delay, change the Delay Time.
* Add some modulation, change the Modulation Depth, Modulation Frequency, and Modulation Wave.

Note: The modulation wave changes from a Saw Wave to a Sine wave to a Reverse Saw Wave. When the full Saw waves are used, the modulation can appear to be a frequency change up or down.

For a standard "stereo delay" the knobs used would be:

Matrix Mixer
* Row 1 Column 7: (U6 to U0) Input from Left Audio Input to Delay 0
* Row 1 Column 1: (U0 to U0) Feedback for Delay 0 into Delay 0
* Row 7 Column 1: (U0 to U6) Output from Delay 0 to Left Audio Output
* Row 7 Column 7: (U6 to U6) Direct Input from Left Audio to Left Audio Output
* Row 2 Column 8: (U7 to U1) Input from Right Audio Input to Delay 1
* Row 2 Column 8: (U1 to U1) Feedback for Delay 1 into Delay 1
* Row 8 Column 1: (U1 to U7) Output from Delay 1 to Right Audio Output
* Row 8 Column 8: (U7 to U7) Direct Input from Right Audio to Right Audio Output
    
Delay Page
* Turn up the Delay time and modulation options for Delay 0 (MD U0)
* Turn up the Delay time and modulation options for Delay 1 (MD U1)

### For a shorter description of the EchoMatrix controls and review:

What are the Units:
 * "Unit 0" to "Unit 5", or "U0" to "U5" - Six Delays, Delay 0 to 5
 * "Unit 6", or "U6" - Left Audio Channel
 * "Unit 7", or "U7" - Right Audio Channel

Delays Tab:
 * "Delay Time" Group - Contains Delay Time controls for each unit (DT U#)
 * "ModFreq" Group - Contains Modulation Frequency controls for each unit (MF U#)
 * "ModDepth" Group - Contains Modulation Depth controls for each unit (MD U#)
 * "ModWave" Group - Contains Modulation Wave "Morph" controls for each unit (MW U#)

MatrixMixer Tab:
 * "Unit # Out" Column - Controls in the column output from Unit # to input to other Units
 * "Ui to Uo" Controls - Controls the volume that "Unit i" (Ui) will input into "Unit o" (Uo)
 * For Example:
    * "U0 to U0" will feedback Unit 0 (Delay 0) into itself (Delay 0 Output to Delay 0 Input)
    * "U6 to U6" will feed Unit 6 into Unit 6 (Left Audio Input to Left Audio Output)
    * "U0 to U6" will output from Unit 0 (Delay 0) to Unit 6 (Left Audio Output) 

Using the Controls
 * Turn the dial or click into label box and enter a value. You can tab from label to label.

## A few control setups to try

### Simple Stereo Delay

Use the first two delay units (U0,U1) and feed them back into themselves.
Input into the delays from left(U6) and right(U7)
Output from the delays (U0,U1) and inputs (U6,U7) into left(U6) and right(U7)
You can vary the delay times, or add a little modulation to add some width
	
 * Delays Tab
    * DT U0: 250 msec
    * DT U1: 250 msec
 * MatrixMixer Tab
    * U0 to U0: 0.5
    * U1 to U1: 0.5
    * U6 to U0: 1.0
    * U7 to U1: 1.0
    * U0 to U6: 0.75
    * U1 to U7: 0.75
    * U6 to U6: 0.75
    * U7 to U7: 0.75

![Simple Delay](https://github.com/improvoid/EchoMatrix/raw/main/Images/BasicDelayFlowDiagram.png)

### Simple Ping Pong Delay

Like the Simple Stereo Delay, but delay units feed back into each other.
U1 feeds back into U0, U0 feeds back into U1
	
 * Delays Tab
    * DT U0: 250 msec
    * DT U1: 250 msec
 * MatrixMixer Tab
    * U0 to U1: 0.5
    * U1 to U0: 0.5
    * U6 to U0: 1.0
    * U7 to U1: 1.0
    * U0 to U6: 0.75
    * U1 to U7: 0.75
    * U6 to U6: 0.75
    * U7 to U7: 0.75

![Ping Pong Delay](https://github.com/improvoid/EchoMatrix/raw/main/Images/PingPongDelayFlow.png)

### Chorus/Flange into Delay

Uses U0 and U1 as short modulated delays into U2 and U3 for the longer delay.
 Modulation frequencies differ a little for more stereo spread.
 Feeds the chorus directly out and also to the delay.
 Delay times in the Delays Tab could be changed a bit for more width
	
 * Delays Tab
    * DT U0: 25 msec
    * DT U1: 25 msec
    * DT U2: 250 msec
    * DT U3: 250 msec
    * MF U0: .4
    * MF U1: .5
    * MD U0: .2
    * MD U1: .2
  * MatrixMixer Tab
    * U0 to U0: 0.5
    * U0 to U2: 1.0
    * U1 to U1: 0.5
    * U1 to U3: 1.0
    * U2 to U2: 0.5
    * U3 to U3: 0.5
    * U6 to U0: 1.0
    * U7 to U1: 1.0
    * U0 to U6: 0.75
    * U1 to U7: 0.75
    * U2 to U6: 0.75
    * U3 to U7: 0.75
    * U6 to U6: 0.75
    * U7 to U7: 0.75

![Chorus Into Delay](https://github.com/improvoid/EchoMatrix/raw/main/Images/DelayAndFlangeFlow.png)

## MODIFICATIONS THAT YOU MAY WANT TO DO

These can all be done using the Faust IDE. EchoMatrix.dsp is commented fairly well and the instructions below can be used to generate source and compile a new version of EchoMatrix.

 * Change the number of effect units, more or less
 * Change the maximum delay time
 * Change the ranges and default values for the controls
 * Add other DSP elements to the Effect

## FEATURES THAT DID NOT MAKE IT INTO THIS VERSION

 * Macro controls: Create macro controls that can control multiple UI controls at the same time.
 * Preset management:  Save, load, and morph between presets.
 * UI enhancement: A more visually interesting UI.
 * Additional effects: Other effects in each "effect" section that can be turned on and off.
 * Tempo Sync to Host
 * Create a custom Faust architecture file to generate less "unused" code
 * Better modulation wave control, full Saw and full Reverse Saw can cause clicks

Development is still active, and some of these should be available soon.

## TO TEST THE DSP THROUGH THE FAUST IDE

* I used Microsoft Edge, It seems to work a little bit better with the Faust IDE
 * Navigate to: https://faustide.grame.fr/
 * Select "Upload" from the Faust IDE (image of line with up-arrow)
 * Navigate to EchoMatrix.dsp, in my case in C:\Projects_Audio\GIT\EchoMatrix\EchoMatrix.dsp
 * Select "Open"
 * The Faust IDE will remember the last .dsp that was opened, and have it open when you load the IDE
 * The result should be like the Faust IDE screen shot below: 
 * You should see the "process" diagram at the bottom, this means everything compiled correctly
   * There is another section of this document that will go over the process diagram
   * But you can just click it to see different "levels" of the DSP effect
 * You can play with the plugin using the IDE by clicking "Run" and playing the Audio File (with loop set)
 * The IDE will show the plugin UI in the bottom window, you may need to make it a bit bigger to use it.
 * The "default" settings of the plugin UI will generate no sound output.
 * To get output for a simple stereo delay:
   * Change the Delays tab to look like this: (IMAGE_2)
   * Change the MatrixMixer tab to look like this: (IMAGE_3)
   * Note the changes in all 4 corners of the MatrixMixer.
      * Left upper corner = Feedback into Delay 1 and Delay 2
      * Right upper corner = Input from Left and Right into Delay 1 and Delay 2
      * Left bottom corner = Output into Left and Right from Delay 1 and Delay 2
      * Right bottom corner = Output to mix Left and Right input into Left and Right output
    * You can also play with the ModDepth on the Delays tab to get some effects

Here is what the Faust IDE looks like:

![FaustIDE](https://github.com/improvoid/EchoMatrix/raw/main/Images/Faust_IDE.png)

Looking into the DSP effect using the diagram window is great:

![FaustDiagram](https://github.com/improvoid/EchoMatrix/raw/main/Images/MatrixDelays.png)

Here is EchoMatrix running in the Faust IDE, Delays Tab:

![FaustDelaysTab](https://github.com/improvoid/EchoMatrix/raw/main/Images/Faust_Delays_Tab.png)

Here is EchoMatrix running in the Faust IDE, MatrixMixer Tab:

![FaustMatrixMixerTab](https://github.com/improvoid/EchoMatrix/raw/main/Images/Faust_MatrixMixer_Tab.png)

## TO GENERATE THE JUCE PROJECT

* Select "Export" from the Faust IDE (image of truck)
* Select Platform -> juce (notice, many other options are available)
* Select Architecture -> plug-in
* Select "Compile"
* After it has compiled, a download button will appear
* Select "Download"
  * By default the download will be called "binary.zip"
  * You can rename it to "EchoMatrix_Juce.zip"
* Create a development directory
  * In my case it was "C:\Projects_Audio\GIT\EchoMatrix"
  * Unzip the zip to a sub directory, in my case EchoMatrix
  * So there is a EchoMatrix sub directory with the 2 files in it
  * EchoMatrix.jucer - The Projucer file to create the JUCE projects
  * FaustPluginProcessor.cpp - The source code for the default IDE and DSP.
  * The .cpp file contains a LOT of code, most of it is not used.

## TO BUILD THE JUCE PROJECT IN WINDOWS

* Download and install JUCE per the JUCE docs - Currently using version 6.0.8
  * You may have to sign up for a developer account and get a free license
  * You may need to download and install the free VST3 SDK. I installed to C:\SDKs\VST_SDK\..
* Run the Projucer.
  * It should be in the directory where JUCE was installed. In my case C:\Projects_Audio\JUCE\Projucer.exe
  * You may have to select "More..." and "Run Anyway" because of Windows 10 security.
  * If you install, the extension .jucer may automatically run Projucer.
* Open EchoMatrix.jucer where you put it.
* Some options should be changed using the gear at the top:
  * Company name stuff - optional
  * Plugin Characteristics - Uncheck everything, no midi input or output for now, not a synth
  * Plugin Channel Configurations - change to {2,2}
* Under Exporters select -> Visual Studio 2019 (you can use the "free" version)
  * Click the round button at the top next to the Selected exported combo box
  * "Saving" should come up, VS2019 should launch with an appropriate project to compiled
  * This may take a while ...
* In Visual Studio 2019
  * Three projects should show up in the EchoMatrix solution
  * Right click the EchoMatrix_VS3 project and select "Set as Startup Project"
  * Right click the EchoMatrix_VS3 project and select "Properties"
  * Under "Debugging" set the command to run the VST host of your choice, in my case I use the JUCE AudioPluginHost.
  * Compiling this is described elsewhere, but any VST host that you can use to load the resulting VST3 will work.
* Changes need to be made to FaustPluginProcessor.cpp contained in the EchoMatrix_SharedCode project (The source code as generated, does not really work as it should, also some cosmetic colors need to be changed a bit).
  * Contained in EchoMatrix_SharedCode>EchoMatrix>Source>FaustPluginProcessor.cpp
  * Search for "struct uiConverter"
  * Comment some code out:

```
    uiConverter(MetaDataUI::Scale scale, FAUSTFLOAT umin, FAUSTFLOAT umax, FAUSTFLOAT fmin, FAUSTFLOAT fmax)
    {
        /* !NOTE! CHANGED: NOT CORRECT, JUST WANT THE CONTROLS SKEWED TOWARD ONE PART OF THE RANGE, NOT VALUES CHANGED
        // Select appropriate converter according to scale mode
        if (scale == MetaDataUI::kLog) {
            fConverter = new LogValueConverter(umin, umax, fmin, fmax);
        } else if (scale == MetaDataUI::kExp) {
            fConverter = new ExpValueConverter(umin, umax, fmin, fmax);
        } else {
            fConverter = new LinearValueConverter(umin, umax, fmin, fmax);
        }
        */

        //Just use linear in all cases
        fConverter = new LinearValueConverter(umin, umax, fmin, fmax);
    }
```	
  * Search for "switch (scale)"
  * Change the skew factors (they are not correct)
```	
	// !NOTE! CHANGED: USED DIFFERENT SKEW FACTORS, NO cLog CONTROLS ARE USED FOR NOW
	switch (scale) {
		case MetaDataUI::kLog:
			fSlider.setSkewFactor(1.5);
			break;
		case MetaDataUI::kExp:
			fSlider.setSkewFactor(0.5);
			break;
		default:
			break;
	}
```  
  * Search for "juce::TabbedComponent::addTab"
  * Change the color, the default white makes things hard to read. Other colors could be better as well.
```
	// !NOTE! CHANGED COLOR FROM white TO deepskyblue
	juce::TabbedComponent::addTab(comp->getName(), juce::Colours::deepskyblue, comp, true);
	comp->setName("");
```
  * Search for "if (FAUST_INPUTS == 0)"	
  * Comment out the whole if statment starting with:

```
	if (juce::PluginHostType::getPluginLoadedAs() == wrapperType_Standalone) {
```	
  * And add below it (or replace the code ...)
```	
	// Manual change to comply with VST3 requirements
	return BusesProperties()
		.withInput("Input", juce::AudioChannelSet::stereo(), true)
		.withOutput("Output", juce::AudioChannelSet::stereo(), true);
```
* Now you should be able to compile the code, and your host will start up.
* To load the VST3 into your host:
  * You will either need to add a path to where the VST3 was built to your host
    * In my case I added C:\Projects_Audio\GIT\EchoMatrix as a VST3 search directory
    * OR copy the VST3 to the correct directory, in my case "C:\Program Files\Common Files\VST3"
  * The "debug" version of the VST3 is in ..\Builds\VisualStudio2019\x64\Debug\VST3\echomatrix.vst3
  * The "Scan for new VST3" option of your host should be used.
  * The VST should show up in the list in a "host dependent" location
  * In the case of the JUCE AudioPluginHost it shows up under the name you put in for the company/echomatrix.
  * Every time you want to use a new version of the plugin, it should be re-scanned.
* Now you can play with the plugin you just compiled.  If errors occur, the VS2019 debugger can debug the VST3
* To generate the "final" version, compile it using "Release" rather than "Debug"

## TO DEBUG USING THE JUCE AudioPluginHost

Compile Extras\AudioPluginHost
* Modify the header file InternalPlugins.cpp.
* These changes remove the requirement for the "Assets" directory and makes it simpler to run AudioPluginHost.exe from any directory.
	
Comment out (with //):

```
//#include "../../../../examples/Plugins/AUv3SynthPluginDemo.h"
#include "../../../../examples/Plugins/ArpeggiatorPluginDemo.h"
#include "../../../../examples/Plugins/AudioPluginDemo.h"
//#include "../../../../examples/Plugins/DSPModulePluginDemo.h"
#include "../../../../examples/Plugins/GainPluginDemo.h"
#include "../../../../examples/Plugins/MidiLoggerPluginDemo.h"
//#include "../../../../examples/Plugins/MultiOutSynthPluginDemo.h"
#include "../../../../examples/Plugins/NoiseGatePluginDemo.h"
//#include "../../../../examples/Plugins/SamplerPluginDemo.h"
#include "../../../../examples/Plugins/SurroundPluginDemo.h"
```

Comment out (with //):

```
        [] { return std::make_unique<InternalPlugin> (std::make_unique<ReverbPlugin>()); },

//        [] { return std::make_unique<InternalPlugin> (std::make_unique<AUv3SynthProcessor>()); },
        [] { return std::make_unique<InternalPlugin> (std::make_unique<Arpeggiator>()); },
//        [] { return std::make_unique<InternalPlugin> (std::make_unique<DspModulePluginDemoAudioProcessor>()); },
        [] { return std::make_unique<InternalPlugin> (std::make_unique<GainProcessor>()); },
        [] { return std::make_unique<InternalPlugin> (std::make_unique<JuceDemoPluginAudioProcessor>()); },
        [] { return std::make_unique<InternalPlugin> (std::make_unique<MidiLoggerPluginDemoProcessor>()); },
//        [] { return std::make_unique<InternalPlugin> (std::make_unique<MultiOutSynth>()); },
        [] { return std::make_unique<InternalPlugin> (std::make_unique<NoiseGate>()); },
//        [] { return std::make_unique<InternalPlugin> (std::make_unique<SamplerAudioProcessor>()); },
        [] { return std::make_unique<InternalPlugin> (std::make_unique<SurroundProcessor>()); }
```

You will probably want to build with the ASIO SDK. You will need to download ASIOSDK2 and install it.
You may need to disable VST2 hosting as the VST2 SDK is no longer availble.
Copy to a executable directory of your choosing, in my case C:\APPS\JUCE\AudioPluginHost.exe

You need to enter the path to the AudioPluginHost.exe into the Debugging startup options in Visual Studio 2019 Debugging properties on the VST3 sub-project and set the VST3 sub project as the startup project.

When debugging starts, AudioPluginHost will start up. You will need to edit the plugin list and the scan for new or updated VST3 plugins plugin locations so that the debugging version of the VST3 will be found.

### Edit This Page (If you are allowed to):

[editor on GitHub](https://github.com/improvoid/improvoid.GitHub.io/edit/main/index.md)

