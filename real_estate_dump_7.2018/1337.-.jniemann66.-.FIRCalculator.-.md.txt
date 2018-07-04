# FIRCalculator

FIR filter design tool by Judd Niemann

![Screenshot](https://github.com/jniemann66/FIRCalculator/blob/master/pictures/screenshot1.jpg)

## Synopsis
********
FIRCalculator is a basic DSP Filter designer written in Python, which uses the[ Parks-McClellan/Remez Exhange algorithm ](https://en.wikipedia.org/wiki/Parks%E2%80%93McClellan_filter_design_algorithm)to produce FIR coefficients for use in digital filtering applications.

It supports up to four pass/stop bands.

This tool is good for small-to-medium sized FIR filters (up to 200 taps or so - the Remez algorithm will struggle to converge with more than that)

## Description of Code

FIR Calculator was developed using the [WinPython](https://winpython.github.io/ "WinPython") Python distribution. 

The program source consists of two python files,

**FIRCalculator.py** : The main part of the app

**FIRDesigner.py** : The graphical user interface. It's an automatically-generated file containing all the UI elements, which is the direct output from converting **FIRDesigner.ui** (a Qt designer file) into a python script using the pyuic4 utility

The ui is designed by editing the **FIRdesigner.ui** file in Qt designer.

Executables can be built using [PyInstaller](http://www.pyinstaller.org/ "PyInstaller")

## Motivation

I have recently been doing a lot of work with digital filters, and needed a simple tool to rapidly design and experiment with FIR filters. 

## Installation

If you have a python development environment set up on your computer (eg WinPython), then you should be able to run **FIRCalculator.py** file directly, provided you have the **FIRDesigner.py** file in the same path.

Otherwise, binaries are also included in the file **windows-binaries.zip** file in this repository. Required dlls are in the **required_dlls.zip** folder - you need to copy the dlls into the same path as the executable (I have tried to incorporate all dependencies in the binary distribution. Apologies for the large file sizes !).

(*Note: On your system, you may still need to install additional dlls. If you have any problems with a particular dependency not being included, then I would like to know about it.)* 

## Usage

*Note: Prior knowledge of DSP principles assumed.*

##### Typical usage: #####
- Run the Program (note: it does take a bit of time to start up)
- Choose a filter prototype from the menu as a starting point (it defaults to low-pass anyway) 
- Tweak the parameters as desired
- Press the 'calculate' button 
- Select all the text in the filter coefficients and copy to your clipboard 
- paste the coefficients into your FIR code. (It is assumed that you already know what to do with them!)

I have largely avoided the use of labels on widgets to save some screen real estate. However, all widgets should have tooltips on them to explain their function.

By default, there are two bands, and they are initially set up as a lowpass filter, with the lower band being a passband, and the upper band being a stopband. (Stopbands are created by setting the band's level to 0, and passbands are created by setting the band's level to 1. Intermediate values are also possible, of course. Note: I may make the levels logarithmic-dB in future - I think this would be more useful.)

You can adjust the number of bands from 2-4 using the 'Bands' spinbox. 

Frequencies in the bands represent normalized frequencies, with 0.5 being the Nyquist frequency. If you choose a frequency that overlaps with another band, it will be highlighted in red to indicate an error, which will almost certainly cause the calculation to fail. 

## Building your own executable

This is the technique I have been using:



- from Python Command prompt, run **pyinstaller**:

**pyinstaller --onefile --clean --noupx e:\python_projects\FIRCalculator\FIRcalculator.py**

(note: problems encountered with upx, hence --noupx)

- Ensure you have the Intel MKL dlls present:
	
		libimalloc.dll
		libiomp5md.dll
		mkl_core.dll
		mkl_intel_thread.dll
		mkl_mc3.dll

(Note: You may need other dlls depending on your CPU. The dlls can usually be found in the **core** folder of the NumPy distribution. All the dlls cannot be included in distrubution because of GitHub's 100MB limit !) 

prerequisities:

		WinPython (including Qt, SciPy NumPy, tools etc)
		pyinstaller3.1.1 (problems encountered with 3.1.2)
