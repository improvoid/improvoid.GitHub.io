## Welcome to the ImprovOid GitHub

This repository currently contains some Audio Applications that are Open Source.

## Submission to the Contest - EchoMatrix VST3 for Windows or Mac

This project will be submitted to the KVR Developer Challenge 2021 contest to highlight the power of the Faust DSP development environment and the JUCE framework to create a multi-target VST3.

[Github source is here](https://github.com/improvoid/EchoMatrix)

## Faust and EchoMatrix

Faust is a powerful functional/mathematical language that can be a little difficult to learn but can create very complex DSP functions.
DSP effect and synthesizer projects can be created rapidly with a minimum amount of code.

One of the great things about Faust, is that you can code a complex DSP function with a small amount of code and modify it to do additional functions easily. These functions can be tested online using either the Faust online editor or the Faust IDE.

There is a great Kadenze course on Faust where some of the original designers and coders of Faust are teaching the course. Without this course, it is unlikely that I would have been able to code EchoMatrix. There is also some courses on JUCE that are good as well, but not really needed to get the basic functionality for EchoMatrix.

Faust can "export" DSP to many different platforms (even IOT devices).  In the case of the EchoMatrix, the Faust DSP code was exported to the JUCE C++ audio VST framework.

The EchoMatrix project is an example of a non-trivial implementation of a Faust DSP algorithm that should provide a good starting point for many possible variations.  I encourage anyone to use and enhance and re-use any part this code. 

## EchoMatrix Quick Description

The EchoMatrix was designed to provide some of the functionality of the Yamaha UD Stomp pedal as used be Alan Holdsworth. The UD Stomp pedal is composed of 8 delays that have a tap and can be modulated and configured to feed into one another to make "longer" delay lines. In the case of Alan Holdsworth, he would use a number of short delays, sometimes slightly modulated, and panned in the stereo sound field to make a very "fat" sound. The EchoMatrix has most of this functionality in a different package. The version of EchoMatrix as submitted only has 6 delays, but can be expanded to 8 delays by changing one line in the source code.  The only issue with adding more delays, is that it adds more controls to the feedback matrix.

(... There is also UD_Delay source and VST3 on my GITHUB that more closely follows the UD Stomp model)

EchoMatrix is a VST3 effect that provides a 6 delays that can be modulated and are connected by a feedback "echo" matrix.  

A "complete" input, feedback, and output mixer matrix of 6 delays and 2 channel input and output are provided so that:
	Inputs can be assigned to any delay at any volume
	Delay output can be sent to any delay input (introducing extra delay or feedback)
	Delay output can be sent to either output channel at any volumne, (so it can pan anywhere in the stereo field)

Delay controls are provided so that:
	Delays can be assigned a delay time
	Delays can be modulated by a morphing wave shape with a variable frequency and modulation amount

This allows flexibility in creating any feedback pattern that you can dream of.

The delays are controlled by "exponential" delay time controls that allows for more short delay time accuracy (by the knobs), but a desired delay can be typed into the input box below the knob. 
 
The UI is entirely defined in the Faust code, and as such is defined by a limited number of options. That is why the "multiple" controls are all defined with numbers starting with 0 (Unit 0, Delay 0 ... in the case of EchoMatrix). This could be modified to be more friendly using manual coding in the JUCE source code, but for now the UI defined by Faust is OK and allows for prototyping other functions for the EchoMatrix easily.

## EchoMatrix UI and Operation 

### SCREEN SHOTS AND DESCRIPTIONS FROM FAUST IDE

The UI at first is a little confusing, but it is "mathematically" consistent because of Faust.

In the Matrix Mixer for 6 delay channels:
	There is an 8 x 8 Matrix Mixer.
	Each of the first 6 rows, row 1 to row 6 (Unit-0 to Unit-5), are the inputs to each of the 6 delay lines.
	The last 2 rows, row 7 and row 8 (Unit-6 and Unit-7), are the "input" to the "Left Audio Output" and the "Right Audio Output".
	Each of the first 6 Columns, column 1 to column 6 (Unit-0 to Unit-5), are the outputs from each of the 6 delay lines.
	The last 2 columns, column 7 and column 8 (Unit-6 and Unit-7), are the "output" from the "Left Audio Input" and the "Right Audio Input".

To make the numbers more consistent in the following description, lets number the delays from 0 to 5,
So the 1st delay is called Delay-0 or Unit-0 and the 6th delay is Delay -5 or Unit-5.
The "Left Audio Channel" corresponds to Unit-6 and the "Right Audio Channel" corresponds to Unit-7.

This means that to "connect" the Left Audio Input (Unit-6) to the input of Delay-0 (Unit-0), the knob in the column 7 and row 1 needs to be turned up. The amount that it is turned up determines the amount of the "Left Audio Input" that will be fed into Delay-0. To send the output from Delay-0 to the "Left Audio Output", the knob in the column 1 and the row 7 needs to be turned up. The amount of signal output from Delay-0 to the Left Audio Output is controlled by the knob.

To provide feedback in Delay-0 (Unit 0), turn up the knob in the Matrix Mixed row 1 and column 1. This will feed the output of Delay-0 (Unit 0) into the input of Delay-0 (Unit 0).

To mix some of the non-delayed "Left Audio Input" (Unit-6) into the "Left Audio Output" (Unit-6) the knob in column 7 and row 7 must be turned up. 

To get the delay effect to work as expected, the Delay tab needs to be used:

Change the length of the delay, change the Delay Time.
Add some modulation, change the Modulation Depth, Modulation Frequency, and Modulation Wave.

Note: The modulation wave changes from a Saw Wave to a Sine wave to a Reverse Saw Wave. When the full Saw waves are used, the modulation can appear to be a frequency change up or down.

For a standard "stereo delay" the knobs used would be:
	Matrix Mixer
		Row 1 Column 7: Input from Left Audio Input to Delay-0
		Row 1 Column 1: Feedback for Delay-0 into Delay 0
		Row 7 Column 1: Output from Delay-0 to Left Audio Output
		Row 7 Column 7: Direct Input from Left Audio to Left Audio Output
		Row 2 Column 8: Input from Right Audio Input to Delay-1
		Row 2 Column 8: Feedback for Delay-1 into Delay-1
		Row 8 Column 1: Output from Delay-1 to Right Audio Output
		Row 8 Column 8: Direct Input from Right Audio to Right Audio Output
	Delay Page
		Turn up the Delay time and modulation options for Delay-0
		Turn up the Delay time and modulation options for Delay-1

## FEATURES THAT DID NOT MAKE IT INTO THIS VERSION

Macro controls: Create macro controls that can control multiple UI controls at the same time.
Preset management:  Save, load, and morph between presets.
UI enhancement: A more visually interesting UI.
Additional effects: Other effects in each "effect" section that can be turned on and off.
Tempo Sync to Host

Development is still active, and some of these should be available soon.

## REQUIREMENTS TO COMPILE.

Download ASIOSDK2

Download and extract JUCE.
Run ProJucer, open C:\Projects_Audio\JUCE\extras\AudioPluginHost
Add C:\SDKs\ASIOSDK2.3.2\common To Header Search Paths
In Modules->juce_audio_devices: Enable JUCE_ASIO
Open with Visual Studio 2019 exporter

### TO TEST THE DSP THROUGH THE FAUST IDE

### TO GENERATE THE JUCE PROJECT

### TO BUILD THE JUCE PROJECT IN WINDOWS

### TO BUILD THE JUCE PROJECT IN OSX

### TO DEBUG USING THE JUCE AudioPluginHost

Compile Extras\AudioPluginHost
	Modify the header file InternalPlugins.cpp. This removes the requirement for the "Assets" directory
	and makes it simpler to run AudioPluginHost.exe from any directory.
	
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

Build with ASIO if you can, using the ASIOSDK2. You may need to disable VST2 hosting.
Copy to a executable directory of your choosing, in my case C:\APPS\JUCE\AudioPluginHost.exe


### Edit

[editor on GitHub](https://github.com/improvoid/improvoid.GitHub.io/edit/main/index.md)

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
