# a07g-exploring-the-CLI

* Team Number: 9
* Team Name: Shorts & Sparks
* Team Members: James Steeman and Timothy Zhang
* GitHub Repository URL: [https://github.com/ese5160/final-project-a07g-a14g-t09-shorts-sparks](https://github.com/ese5160/final-project-a07g-a14g-t09-shorts-sparks)
* Description of test hardware: Macbook pro m2 (macOS) and lab desktops (windows) (development boards, sensors, actuators, laptop + OS, etc)

## 0 Install Percepio

## 1 Software Architecture

Note All HRS and SRS are currently just from a00g, no updates made

test a main addition

### Hardware Requirements Specification (HRS)

#### H.1 Overview

In normal operation, the router will be powered from a wall outlet, simultaneously charging the backup battery if necessary. On a power outage, the power source will switch to the battery. On detecting this switch the motors will not operate and the job will be paused.

The router will have motors to control the orientation of the material being shaped and the position and speed of a drill bit that will perform the subtractive manufacturing operation. In total, the router will use 4 motors: three stepper motors and 1 DC motor. The DC motor will control the speed of the drill bit rotation. One stepper will be attached along the z axis of the cyllindrical material, and this motor will control its theta axis or rotational orientation. The drill bit will be perpendicular to both the z axis of the material and the plane of the macine base plate. One stepper will act as a linear actuator, rotating a threaded rod that is parallel to the material z axis and ofset above the material. This linear actuaor also holds the drill bit jig, thereby moving the head of the drill bit. The final stepper motor will similarly act as a linear actuator to move the drill bit up and down in the direction it points.

We plan on using encoders as sensors on each stepper motor. We would like to design a custom closed loop feedback PCB (1 per motor in final assembly). This board would include a motor driver, an additional MCU, and a thermistor.

There were be a micro SD card to hold the cnc instruction file (G-code). This is also where current job progress will be stored in any pausing scenario.

#### H.2 Definitions, Abbreviations

| Term   | Definition                                                                          |
| ------ | ----------------------------------------------------------------------------------- |
| CNC    | Computer Numerical Control                                                          |
| G-code | set of instructions a CNC controller uses to tells the motors where and how to move |

#### H.3 Functionality

| Req ID | Requirement | Review |
| ------ | ----------- | ------ |
| HRS-01 | The CNC router shall use 3 stepper motors to control one rotational axis and 2 linear axis (cylindrical coordinates) | N/A |
| HRS-02 | The CNC router shall use 1 DC motor for spindle                                                                                                     | N/A    |
| HRS-03 | The system shall have external non-voilatile memory (microSD) of no less than 512MB for storing G-code and current progress (in any pause scenario) | N/A    |
| HRS-04 | The CNC router shall be able to cut foam material                                                                                                   | N/A    |
| HRS-05 | The CNC shall have a milling volume of 300cm^3 (similar to a can of coke)                                                                           | N/A    |
| HRS-06 | The CNC shall run off a wall outlet during operation                                                                                                | N/A    |
| HRS-07 | The CNC shall run off a single cell Li-Ion battery (3.7V nominal voltage) during power outage (sleep mode)                                          | N/A    |
| HRS-08 | The system shall use the SAMW25 as the microcontroller and Wi-Fi communication IC                                                                   | N/A    |
| HRS-09 | The stepper motors shall use encoders for closed loop feedback                                                                                      | N/A    |
| HRS-10 | The system shall have status indicator LEDs on the PCB                                                                                              | N/A    |
| HRS-11 | The system shall have a power (on/off) switch                                                                                                       | N/A    |

### Software Requirements Specification (SRS)

#### S.1 Overview

The user interface will contain a upload portal to send the machining file. It will also contain some matchine settings that the user will adjust before beginning the job. The interface will have control button such as start and pause. There will also be status details such as idle/waiting for a job, actively running, finished job on machine, and paused due to power outage.

On a power outage, the job will be paused. The current state of the system will be stored, and upon restoration of primary power, router motors will reset and restore the proper position.

The addition MCUs in the closed loop stepper motor module will run on bare metal to process the encoder data in a control loop. The main board's MCU (running the RTOS) will communicate with each of these boards over I2C, sending the sub-instructions to each motor's MCU from the overall g-code that determines all of the necessary operations. This MCU will then interface with the motor controller, including the feedback loop. The thermistor will be used to monitor thermals.

The G-code instructions, stored on the micro SD card, will be iteratively accessed (SPI) and distributed as the machine operates.

#### S.2 Users

The users of our product are makers. From hobbyists simply looking to see their designs in real life to designer seeking rapid prototyping, our CNC router gets the job done. **By Makers. For Makers.**

#### S.3 Definitions, Abbreviations

| Term  | Definition                   |
| ----- | ---------------------------- |
| OTAFU | over the air firmware update |
| RTOS  | real time operating system   |

#### S.4 Functionality

| Req ID | Requirement | Review |
| ------ | ----------- | ------ |
| SRS-01 | The system shall be able to control all 3 stepper motors in its cyllindrical coordinates | N/A    |
| SRS-02 | The MCU in the SAMW25 module shall run an RTOS | N/A    |
| SRS-03 | The user shall be able to remotely operate the machine, setting presets, start/pause etc | N/A    |
| SRS-04 | The system shall be able to send status updates and job progress to the web portal for the user | N/A    |
| SRS-05 | The system shall be able to read and interoperate encoder values as positions | N/A    |
| SRS-06 | The system shall be able to automatically pause the job when power loss/overheat | N/A    |
| SRS-07 | The system shall be able to perform zeroing (calibration) | N/A    |
| SRS-08 | The system shall be able to resume job from any paused state | N/A    |
| SRS-09 | The user should be able to upload job file remotely through a portal on webpage | N/A    |
| SRS-10 | An OTAFU should be implemented | N/A    |

### Block Diagram for software tasks

temp

### Flowcharts and State Machines

temp

## 2 Understanding the Starter Code

1. What does “InitializeSerialConsole()” do? In said function, what is “cbufRx” and “cbufTx”? What type of data structure is it?
2. How are “cbufRx” and “cbufTx” initialized? Where is the library that defines them (please list the *C file they come from).
3. Where are the character arrays where the RX and TX characters are being stored at the end? Please mention their name and size.
Tip: Please note cBufRx and cBufTx are structures.
4. Where are the interrupts for UART character received and UART character sent defined?
5. What are the callback functions that are called when:
   1. A character is received? (RX)
   2. A character has been sent? (TX)
6. Explain what is being done on each of these two callbacks and how they relate to the cbufRx and cbufTx buffers.
7. Draw a diagram that explains the program flow for UART receive – starting with the user typing a character and ending with how that characters ends up in the circular buffer “cbufRx”. Please make reference to specific functions in the starter code.
8. Draw a diagram that explains the program flow for the UART transmission – starting from a string added by the program to the circular buffer “cbufTx” and ending on characters being shown on the screen of a PC (On Teraterm, for example). Please make reference to specific functions in the starter code.
9. What is done on the function “startStasks()” in main.c? How many threads are started?

## 3 Debug Logger Module

Commit your functioning Debug Logger Module to your GitHub repo, and make comments that are in Doxygen style.

## 4 Wiretap the convo

### Questions

1. What nets must you attach the logic analyzer to? (Check how the firmware sets up the UART in SerialConsole.c!)
2. Where on the circuit board can you attach / solder to?
3. What are critical settings for the logic analyzer?

### Hardware Photo

Submit a photo of your hardware connections between the SAMW25 Xplained dev board and the logic analyzer.

### Decoded Screenshot

Submit a screenshot of the decoded message.

### Small Capture .sal file

Submit a small capture file (i.e., the .sal file) of a wiretapped conversation (you don’t need to log 30 minutes worth of UART messages 🙂)

## 5 Complete the CLI

Commit your functioning CLI code to your GitHub repo, and make comments that are in Doxygen style.

## 6 Add CLI commands

### Code

Commit your functioning CLI code to your GitHub repo, and make comments that are in Doxygen style.

### Video Link

Submit a link to a video of this functionality in your README.md

## 7 Using Percepio

Submit a screenshot of your Percepio trace in your README file.
