# About
Python (3.8) code that runs on your PC or RPi, interacts with [OpenScope MZ](https://reference.digilentinc.com/reference/instrumentation/openscope-mz/start) (by digilent) over WiFi to automate the process of collecting data from openscope

This code could in RPi and the combo RPi+OpenScope becomes your own smart / automated oscilloscope / Data Acquisition System.

You might want to read this before coding on top this repo : [Digilent Instrumentation Protocol](https://reference.digilentinc.com/reference/software/digilent-instrumentation-protocol/protocol)
# Files
## OpenScope115200.hex
* The standard baudrate this device uses is 1250000 but if usually devices have max baudrate of 115200 
* For OpenScope to communicate with such devices, install this firmware 
**PROCEED WITH CAUTION**
    * This is process is not reversible (same way as uploading firmware)
    * digilent-agent and wavesform live won't work as baud rate will be changed 
    * To reverse the process, see "Reverting to original firmware" below

###Install my firmware
```
1. Hold BTNP and press BTNR on device to go into bootloader mode
2. Download OpenScope115200.hex 
3. Follow Update OpenScopeMZ firmware (link below)
4. While step#2 In "Available Firmware Versions" Select option "Others" to browse and pick downloaded file.
```
[Update OpenScopeMZ firmware](https://reference.digilentinc.com/learn/instrumentation/tutorials/openscope-mz/update-firmware)

###Revert to Original Firmware
```
0. Install Arduino 1.6.9
1. Follow instrunctions at OpenScopeMZ source code github repository markdown 
(link to repo given below)
2. Don't forget to put device in bootloader mode before arduino upload !
```
[Digilent/openscope-mz](https://github.com/Digilent/openscope-mz)

## usb_omz.py 
* Sets up parameters like sampling rate, sample size and number of acquisitions to be done and wait interval between the acquisitions
* Script takes maxacqCount number of acuisition in different files and saves it as CSV files.
## decode.py 
* Finds all data container files in current diectory generated by usb_omz.py
* Decodes bin files to csv format
## Problems
* Sadly Digilent Openscope has been discontinued. 
* At high sample size, I observed that only 90% is data collected and there is a data loss while reading data from serial input. This problem might be solved by placing right serial object parameters. [Forum Question](https://forum.digilentinc.com/topic/20989-oscilloscope-read-fails-at-high-sample-sizes-greater-than-~3900-samples/)
