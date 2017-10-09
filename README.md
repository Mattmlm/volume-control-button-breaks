# Purpose

This is a modified project based on echoTouch code from Apple. It has been modified to include buttons to manipulate the AVAudioSession, in order to demonstrate reproducable bugs with the voice processing audio unit for iPhone 8.

# Bug

When using a voice processing audio unit, if an application gives up the audio session to another app (i.e. Google Hangouts phone call) or programattically ([AVAudioSession.sharedInstance setActive: NO]), the volume control buttons on the phone will stop changing the volume for the speakers audio route.

# Reproduction Steps

Build the echoTouch app on an iPhone 8 or iPhone 8+.

1. Open app.
2. Press "Record", and record a steady sound at unchanging volume.
3. Press "Play"
4. While recorded sound is playing, adjust the volume up and down.

Observation:
Volume control works fine, the volume of the recorded sound goes up and down.

5. After pressing "stop", or waiting until sound finishes playing, press setActiveNO button.
6. Wait at least two seconds
7. Press setActiveYES again, to restart the audio unit.
8. Press play again
9. While sound is playing, adjust the volume up and down.

Expectation:
Volume control works fine, the volume of the sound goes up and down according to the controls.

Actual:
Volume control does not work, the displayed volume is ignored, and the audio plays at a single static level.

# echoTouch

echoTouch demonstrates using the Voice Processing I/O audio unit for handling audio input and output. The application tests local audio playback and simulated "far-talker" audio playback allowing you to record and listen back to the results. It also lets you to turn on/off the VPIO comparing the recorded results.

The Voice Processor I/O audio unit was discussed in the WWDC Session "Fundamentals of Digital Audio for Mac OS X and iPhone OS" which can be found here: < https://developer.apple.com/devcenter/download.action?path=/videos/wwdc_2010__sd/session_411__fundamentals_of_digital_audio_for_mac_os_x_and_iphone_os.mov >

## Main Files

ViewController.mm
- Source for the main sample implementation.

ViewController.h
- Header for main controller class.

echoTouchHelper.cpp
- Utility functions for setting up the I/O unit, AVAudioSession and loading data for the simulated input audio.

echoTouchHelper.h
- Headear for echoTouchHelper.cpp

echoTouchAppDelegate
- Standard App delegate files.

MeteringViews Folder
- Classes implementing the VU meters.

PublicUtility Folder
- AUOutputBuffer class
- CAStreamBasicDescription class

Audio Folder
- fx.caf : Sound Effects audio file.
- sampleVoiceXXXkHz.wav : Simulated far-talker audio files at various sample rates.

## Requirements

### Build

Xcode 8.0, iOS 10 SDK

### Runtime

macOS 10.11.6 or greater
iOS 9.3 or greater
