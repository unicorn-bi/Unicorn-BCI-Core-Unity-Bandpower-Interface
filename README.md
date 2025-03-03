# Unity Bandpower Interface

Unity Bandpower Interface is a seamless Unity plugin designed for developers working with Unicorn BCI Core devices. It enables real-time bandpower calculation, allowing effortless integration of bandpower-based BCI games and applications. With an intuitive setup and optimized performance, this interface empowers developers to create immersive, brain-driven experiences with ease. 

[Prerequisites](#Prerequisites)<br/>
&nbsp;&nbsp;&nbsp;[Hardware Requirements](#hardware-requirements)<br/>
&nbsp;&nbsp;&nbsp;[Development](#development)<br/>
&nbsp;&nbsp;&nbsp;[Deployment](#development)<br/>
[Prefabs](#prefabs)<br>
&nbsp;&nbsp;&nbsp;[Device](#device)<br>
&nbsp;&nbsp;&nbsp;[Connection Dialog](#connection-dialog)<br>
&nbsp;&nbsp;&nbsp;[Logger](#logger)<br>
&nbsp;&nbsp;&nbsp;[SQ Bar](#sq-bar)<br>
&nbsp;&nbsp;&nbsp;[Bandpower Bars](#bandpower-bars)<br>
[Quickstart Guide](#quickstart-guide)<br/>
[Deploy to Windows]()<br/>
[Deploy to macOs]()<br/>
[Deploy to Android]()<br/>

# Prerequisites

## Hardware Requirements
- Development: Windows or Mac computer
- Deployment: Windows, Mac or Android device
- Unicorn BCI Core 8
- Bluetooth adapter supporting Bluetooth 5

## Development

### Windows
- Windows 11
- Unity<br>2022.3.56f1
- NET Framework <br> .NET Framework 4.8
- Visual Studio<br> Microsoft Visual Studio 2022

### Mac
- macOs 14.5+
- Unity<br>2022.3.56f1
- Xcode<br>15.4
- Command Line Tools for Xcode<br>15.3
- Visual Studio Code

## Deployment

### Windows
- Windows 11
- NET Framework <br> .NET Framework 4.8

### Mac
- macOs 14.5+

### Android
- SDK Version 31+

## Prefabs

### Device

<p align="center">
<img src="./img/unity4.png" alt="drawing" width="400"/><br/>
</p>

### Settings

#### Type
- Unicorn BCI Core - Adds Unicorn BCI Core devices to the available devices list
- Simulator - Adds simulator devices to the available devices list
- All Devices - Adds simulator and Unicorn BCI Core devices to the available devices list

It is possible to simulate good, floating or grounded EEG using the simulator devices. It is also possible to simulate alpha activity using the simulator devices.

### Advanced Settings

<p align="center">
<img src="./img/unity5.png" alt="drawing" width="400"/><br/>
</p>

#### Buffer Settings

It is possible to modify the buffersize and buffer overlap used for bandpower calculation. The output rate of calculated bandpower is affected by changing buffersize and buffer overlap.

$$ f_{bandpower} =  {1 \over {(buffersize - bufferoverlap) \over samplingrate}} $$

#### Frequency Ranges

The Unity Bandpower interface is estimating bandpower for various frequency bands. It is possible to modify the cutoff frequencies of each calculated frequency band in the advanced settings.

#### Bandpower Ratios

The Unity Bandpower interface calculates different bandpower ratios from the defined frequency bands. Available ratios are:

$$ PowerRatioIndex =  {delta + theta \over alpha + beta} $$
$$ DeltaAlphaRatio =  {delta \over alpha} $$
$$ ThetaAlphaRatio =  {theta \over alpha} $$
$$ ThetaBetaRatio =  {theta \over beta} $$
$$ ThetaBetaAlphaRatio =  {theta \over alpha + beta} $$
$$ EngagementIndex =  {beta \over theta + alpha} $$

## Events

The device prefab provides an event system as an interface to unity.

### OnDevicesAvailable
The event called when devices are discovered. Available devices are provided as list of strings.
<br>Event data: List&#x003c;string&#x003e;

### OnDeviceStateChanged
The event called when device state changed. Th current device state is provided as 'State' enum.
<br>Event data: List&#x003c;State&#x003e;

### OnPipelineStateChanged
The event called when a signal rocessing pipeline state changed. The current state is provided as string.
<br>Event data: string

### OnRuntimeExceptionOccured
The event called when a runtime exception occured. The Exception is provided as 'Exception' object.
<br>Event data: Exception

### OnBandpowerAvailable
The event called when bandpower values for each channel individually are available. The frequency of the event is affected by the buffer settings and bandpower ranges set in the [Advanced Settings](#advanced-settings). Data is provided as Dictionary with the frequency band name as Key (delta, theta, alpha, beta-low, beta-mid, beta-hig, gamma) and the bandpower values as double array as value.
<br>Event data: Dictionary&#x003c;string, double[]&#x003e;

### OnMeanBandpowerAvailable
The event called when averaged bandpower values over all channels are available. The frequency of the event is affected by the buffer settings and bandpower ranges set in the [Advanced Settings](#advanced-settings). Data is provided as Dictionary with the frequency band name as Key (delta, theta, alpha, beta-low, beta-mid, beta-hig, gamma) and the bandpower value as double value.
<br>Event data: Dictionary&#x003c;string, double&#x003e;

### OnRatiosAvailable
The event called when bandpower ratios for each channel individually are available. The frequency of the event is affected by the buffer settings and bandpower ranges set in the [Advanced Settings](#advanced-settings). Data is provided as Dictionary with the bandpower ratio name as Key (PowerRatioIndex, DeltaAlphaRatio, ThetaAlphaRatio, ThetaBetaRatio, ThetaBetaAlphaRatio, EngagementIndex) and the bandpower ratios as double array as value.
<br>Event data: Dictionary&#x003c;string, double[]&#x003e;

### OnMeanRatiosAvailable
The event called when averaged bandpower ratios over all channels are available. The frequency of the event is affected by the buffer settings and bandpower ranges set in the [Advanced Settings](#advanced-settings). Data is provided as Dictionary with the bandpower ratio name as Key (PowerRatioIndex, DeltaAlphaRatio, ThetaAlphaRatio, ThetaBetaRatio, ThetaBetaAlphaRatio, EngagementIndex) and the bandpower ratio as double value.
<br>Event data: Dictionary&#x003c;string, double&#x003e;

### OnSignalQualityAvailable
The event called when new signal quality values are available.
<br>Event data: List&#x003c;ChannelStates&#x003e;

### OnBatteryLevelAvailable
The event called when battery level data is available.
<br>Event data: float

### OnDataLost
The event called when data is lost.
<br>Event data: None

## Quickstart Guide

1. Create a new Unity Project

<p align="center">
<img src="./img/unity1.png" alt="drawing" width="750"/><br/>
</p>

2. Import the Unity Bandpower Interface unity package.<br>
Click Assets -> Import Package -> Custom Package... -> load .unitypackage<br>
Ensure that all items are selected and click 'Import'.

<p align="center">
<img src="./img/unity2.png" alt="drawing" width="200"/><br/>
</p>

3. Open Assets -> Plugins -> gtec -> Bandpower -> Prefabs and drag the [device](#device) Prefab into your Scene

<p align="center">
<img src="./img/unity3.png" alt="drawing" width="750"/><br/>
</p>

4. 