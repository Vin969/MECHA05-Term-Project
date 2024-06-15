


                    **ME-507**


    **Mechanical Control System**

**Design: **

**Term Project**

By Conor Schott and Vinayak Sharath

Department of Mechanical Engineering

California Polytechnic State University, San Luis Obispo



1. **Overview**

This page discusses the completed project for ME-507: Mechanical Control System Design. The memo highlights the major hardware components, software implementation, mathematical modeling, and attachments related to the project.


The project involved the comprehensive process of designing, constructing, programming, testing, and documenting a machine while adhering to given design, manufacturing, and safety constraints. At the core of the project was a custom-designed PCB utilizing the STM32F411 microcontroller, which was programmed in C/C++ via STM32CubeIDE. The machine was to incorporate multiple actuators, such as motors with appropriate drivers, and featured two unique sensors to enhance its functionality and responsiveness. A closedloop control system was to be implemented, utilizing real-time feedback to ensure optimal performance. Furthermore, the machine was to incorporate a “kill-switch” operated from a provided radio receiver to cease all motion/ power to subsystems.


Inspired by the medical device industry, the selected project was to emulate a continuum robotic limb. The field of continuum robotics - usually referred to as soft robotics - became prominent in the engineering realm in the 1990’s. These robots often incorporate fluid actuators such as pistons as well as mechanical actuators like servos and motors. These systems usually require several degrees of tensioning to ensure the robot can balance itself as the lack of rigid links causes balance and load-bearing issues.


The fundamental idea of this project was to create a tendon-driven soft robotic tentacle with a gripper at its end to mimic a user’s arm. The motion of the arm was to be controlled by an Inertial Measurement Unit (IMU) strapped to a glove worn by a user. On this glove was to be a flex sensor to control the gripper when the user’s finger(s) close to the center of the palm.

2. **Major Hardware (Electrical and Mechanical)**
    1. **Design of the Robot/Contraption**

The tentacle’s main operation is compressing/ curling down as well as rotating at its base to emulate vertical and horizontal panning as done by an arm rotating about its elbow. Many designs of a continuum robot utilize equidistant tendons that are tensioned via some actuator to control movement (i.e. 4 tendons along a circular face controlled by servos at its base).


                

<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image1.jpg). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image1.jpg "image_tooltip")



### 
    Figure 1: Main assembly CAD of tentacle in Fusion 360


The design of this project sought out to only use one tensioning actuator in the form of a motor controlled by an encoder. This was partly due to our limited knowledge on the subject as well as our hesitancy to incorporate two motor driver chips in the printed circuit board (PCB) discussed in section 2.4.


The heart of the design centered on the links shown in figure 2 . These served as the robot’s


        

<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image2.jpg). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image2.jpg "image_tooltip")



### 
    Figure 2: Individual link of tentacle


body and had holes spaced out to allow for three cords to run through them, as well as a larger center hole for surgical tubing to hold the links together and promote flexible motion. The center holes at the rounded points of the links were to guide the tensioned cord along a path such that when retracted the robot would curl inward. The two holes on the links back side were meant for cords for balance. The initial design was going to utilize retractable office lanyards since they can vary in length when stretched to a desired position. Due to the lateness of their order as well as a delay in shipping, the design used rubber bands as the balancing cords. The links were designed to be partially flexible and were therefore printed with Thermoplastic polyurethane (TPU) using a Bambu A1 Mini. Printing TPU can be especially challenging if not set up correctly, so many of our links only printed the first several layers, but not the portion with the small extrusions that space out the links.


The gripper’s design was rudimentary in its inception as well as execution. This was also to be printed via TPU, and similarly to the links, it too had a print failure after the first few layers. The ridges on the fingers were meant to be drilled through to slide cord through them that would function similarly to the rest of the arm to compress itself inward to grip items. The cord to drive the motion was to be run through the surgical tubing as to not get in the way of the robots motion. This was not a sound mechanical idea as it became impossible to tension the gripper by means of a servo once it was strung all the way through the tubing.


Other components of the design are visible in figure 1 displaying the full computer aided design (CAD) of the system. The horizontal panning motor was to be stationary and attached to a larger base that supported our PCB as well. It would drive a 1:1 gear train to avoid compressive axial loading on itself, and the driven gear was to support the base for the actual arm. On this higher base were the link/ gripper/ tubing assembly, as well as the second motor that controlled the spool of cord that tensioned the arm.


        

<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image3.jpg). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image3.jpg "image_tooltip")



### 
    Figure 3: Gripper design as part of full assembly


Upon actually building the robot (result shown in figure 4), we found that it could not balance itself, and the use of motors to control may not have been optimal (this will be discussed in section 2.2). While the compressive motor was able to curl the arm inward, spinning it the other direction did not allow the arm to return to its initial position immediately as we thought. Due to the lack of motor control in testing, our robot was susceptible to damaging itself when the motors would continue to spin.

    2. **Motors or Other Actuators**

Describe the motors or other actuators used in your project, including their specifications and role in the overall system. The actuators selected for this project were two GM16 50RPM Metal 12V DC Geared Motor with quadrature rotary encoders and a FITEC FS90R Continuous Servo. The motors were selected due to their size and their stall current of 0.75A. These actuators were selected after our PCB was designed, so we were designing around a 2-2.4A operating range. In hindsight this was not the optimal order of design, as the PCB should support our electrical and mechanical needs, not the other way around. If we were to improve the design of this robot, we would’ve opted for position controlled servos as opposed to motors with encoders and continuous servos. Continuous motion proved to be detrimental during testing due to wires getting tangled up and damaging the physical components and how they were adhered onto the body of the robot. Using standard servos would’ve allowed us to control the tensioning of the robot in a much more logical way without the need for encoders.




<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image4.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image4.png "image_tooltip")


Figure 4: Physical robot featured in live demo



    3. **Sensors**

The sensors used in this project were a BNO055 Inertial Measurement Unit, the quadrature encoders that came with our motors, and a force sensing resistor. The applications of these sensors will be discussed in section 3 in greater detail, but these sensors were to work in tandem with our actuators, with two of them not being present on the robot. The BNO055 and force sensing resistor were to be controlled by a user and housed on a glove. The encoders were to read motor position to allow for position control in tensioning the cords of the system. To reiterate, it would have been more logical to use positional servos to tension the cords due to their nature to only spin a required amount using PWM as opposed to a continuous spin as a result of a given duty cycle. Working with the encoders provided difficulty in our coding structure and ultimately did not work. Another sensor used for this project was the provided DumboRC Radio receiver and transmitter to act as a “kill-switch” for the robot.

    4. **Custom PCB**

The PCB’s primary power features are a 12V Rail, a 5V rail, and a 3V3 internal plane. The process of stepping the voltage down is displayed in figure 6. A reverse polarity circuit was designed in tandem with the primary voltage regulation performed by the ADP2302ARDZ 12-5V Buck Switching regulator.




<p id="gdcalert5" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image5.jpg). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert6">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image5.jpg "image_tooltip")



### 
    Figure 5: PCB designed using Fusion 360


In our final design, however, the inductor was left out of the switching output and caused several problems with our board power. This caused the Low Dropout Voltage (LDO) regulator to fail numerous times since its condition of 5V input was rarely met. We needed to cut traces and bodge-wire a good portion of the power side of the board. This ultimately took up much of our physical working time and caused us to scrap the custom board in favor of the STM32 Black pill which utilized the same chip (STM32F411, albiet with less GPIO).


The motor driver was the most important peripheral on the board since the motion of our robot relied on this. We chose a tb6612fng and attempted to recreate its carrier circuit on our own board. A large problem we encountered was that we were not getting 12V out of the Motor-out pins, thus causing the driver to not actually do anything. This could have been caused by a number of reasons; perhaps we didn’t enable the driver correctly, we could’ve blown out the circuit and didn’t know, and most of all we weren’t sure about the components we were using to ensure its functionality was sound. That was a prevalent theme for this project in general, but we’ve learned more about the purpose of individual electrical components in a circuit through the process of reworking our board for several days. Provided is a figure of the printed circuit board with all components (Crystals, capacitors, regulators and driver, resistors, and headers). The board was given power using a wall adapter with 2A limiting current. Designing this circuit was very illuminating for a plethora of reasons.



<p id="gdcalert6" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image6.jpg). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert7">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image6.jpg "image_tooltip")



### 
    Figure 6: Reverse polarity protection portion of schematic


A primary lesson was how we should have designed this board initially. Reiterating a point from earlier, using servos instead of motors to tension the cords would have eliminated the need for a 12V rail, as most servos function at 4-6V. We could have still used a switching regulator if we so chose, and we could have experimented with stepping a 6V source to 5V for sensors and separately stepping the 6V rail to 3V3 (as opposed from the 5V rail). This would allow for better troubleshooting so all the power going to the mcu doesn’t rely on the power going to the sensors and vice versa.



<p id="gdcalert7" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image7.jpg). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert8">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image7.jpg "image_tooltip")



            Figure 7: 12V to 5V stepping portion of schematic



<p id="gdcalert8" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image8.jpg). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert9">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image8.jpg "image_tooltip")



            Figure 8: 5V to 3V3 stepping portion of schematic



<p id="gdcalert9" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image9.jpg). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert10">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image9.jpg "image_tooltip")



    Figure 9: Physical circuit with all components placed sans the blown out MCU



3. **Software Implementation**

The software implementation played a crucial role in achieving the project goals of developing a soft robotic tentacle with a gripper controlled by an IMU and flex sensor. Here’s a detailed overview of the key components implemented and their contributions to our system:

    5. **FSR Controller (**fsr controller.h/.c**)**

The FSR controller module translated human input to the gripping force of the tentacle gripper. Implemented in fsr controller.h and fsr controller.c, this module was designed to read analog signals from force-sensitive resistors (FSRs). It featured several key functions: the map() function, which scaled and mapped FSR readings to a desired output range, allowing the gripper to respond to varying force levels; the get averaged adc value() function, which sampled and averaged ADC readings to provide stable inputs for the FSRs; and the apply low pass filter() function, which smoothed FSR output using a low-pass filter to ensure precise force detection.


Integrated into the main control loop, the FSR controller enabled real-time monitoring of grip force, enhancing the tentacle’s ability to grasp objects with appropriate force feedback. Placing the FSR sensors on a glove allowed users to control the gripper’s intensity by adjusting the pressure applied. However, challenges arose in ensuring accurate sensor readings due to noise and calibration issues. To improve performance, future iterations of the system could focus on refining calibration techniques and reducing noise interference. Additionally, exploring advanced algorithms for more sophisticated force control would further enhance the tentacle’s gripping capabilities and overall performance in different operational scenarios.

    6. **Receiver (**Receiver.h/.c**)**

The receiver module managed communication with the RC receiver and to cease tentacle and gripper movements. Implemented in Receiver.h and Receiver.c, this module included an isRadioOn function that determined whether the RC receiver was on or off. If the receiver was off, the program would break and end, serving as a kill switch for our robot to ensure safe operation. This safety feature was essential to prevent unintended movements and ensure that the robot would only operate when commanded to do so via the RC receiver. However, issues were encountered with signal interference and occasional signal loss, affecting the reliability of control. For future improvements, implementing signal redundancy and robust error handling mechanisms could enhance the module’s reliability, ensuring consistent and uninterrupted communication between the robot and the RC receiver.

    7. **Motor Driver (**Motor Driver.h/.c**)**

The motor driver module was the core include for our soft robotic tentacle project, facilitating the operation of DC motors by controlling their direction and speed through PWM signals.


Implemented in Motor Driver.h and Motor Driver.c, this module featured functions to enable/disable motors, set motor duty cycles for speed control, and manage PWM channels. Integrated into the main control loop, the motor driver module provided precise control over tentacle movement and gripper actuation, playing a crucial role in achieving accurate and repeatable motion. Specifically, the motors were responsible for controlling the robotic arm’s rotational movement and vertical motion. However, challenges arose in achieving smooth and consistent movement due to variations in motor performance and occasional PWM signal instability. Future improvements could focus on optimizing motor control algorithms and enhancing PWM signal management to ensure more reliable and precise movement control, thereby improving the overall performance of the robotic system.

    8. **BNO055 Sensor Integration (**bno055.h/.c, bno055 stm32.h/.c**)**

The BNO055 sensor integration module acted as the primary controller of the system as it was designed to utilize the motor driver to control the motion of our motors. Implemented in bno055.h and bno055.c, this module included functions to set sensor operation modes, read sensor data (such as temperature, orientation, and system status), perform sensor calibration, and manage sensor communication. Integrated into the main control loop, the BNO055 module provided real-time orientation data that was used to adjust tentacle movement, ensuring the tentacle maintained the correct orientation relative to the user’s hand movements. This capability was fundamental for the overall functionality of the soft robotic tentacle, enabling precise and responsive movement adjustments based on the user’s interactions. However, challenges were encountered in maintaining consistent sensor calibration and occasional communication issues, which impacted the accuracy of orientation feedback. Future improvements could focus on refining sensor calibration routines and optimizing communication protocols to enhance the reliability and accuracy of orientation data, thereby improving the overall performance of the robotic system.

    9. **Main Loop (**main.c**)**

The main.c file serves as the core component of a robotic system, responsible for initializing hardware peripherals, managing control loops, and integrating sensor data. It includes necessary headers and libraries for motor drivers, sensor inputs, and radio receiver inputs. The file defines crucial variables and structures for handling RC receiver configurations, motor control, and sensor data processing, such as FSR pressure detection and BNO055 sensor data. To improve, advanced sensor fusion techniques like Kalman filtering can enhance accuracy, while creating PID parameters and implementing error handling can improve stability and reliability. Enhancements in error handling, debugging mechanisms, and defensive programming techniques can further bolster robustness and reliability, ensuring effective management of hardware and software integration for optimal performance of the robotic system.

    10. **Drivers and Implementations**

Several drivers and implementations were especially notable for their elegance and uniqueness in the project. For instance, the use of the FSR controller to modulate the speed of a servo motor based on grip force was innovative. This was achieved by reading FSR values and mapping them to servo positions, allowing the tentacle gripper to adjust its grasp dynamically. Similarly, using the IMU (BNO055 sensor) to adjust the speed and direction of DC motors based on orientation data was a novel approach.


Unfortunately, there were challenges with implementing encoder-based position control using a proportional controller (PID-control). The motor encoders did not function as expected, possibly due to wiring or hardware issues, which limited our ability to achieve precise motor control. As a result, PID-control by using encoders was not implemented at the end.

    11. **Coding Style**

The project is structured with several files that collectively implement an embedded system application using the STM32 microcontroller platform. The code is organized into modules, starting with the main functionalities in main.c. This file initializes necessary peripherals such as GPIO, DMA, I2C, ADC, and TIM using STM32Cube’s HAL (Hardware Abstraction Layer) functions. It integrates the BNO055 IMU sensor for reading Euler angles, which are filtered using a basic moving average filter and used to control two motors through custom motor driver functions. The application also reads from an ADC to process input from a force-sensing resistor (FSR), applying averaging and low-pass filtering techniques to adjust servo speeds and control motor states based on the ADC values. Real-time debugging and data transmission are facilitated via UART, providing feedback on motor positions, duty cycles, ADC values, and servo speeds. The project incorporates comprehensive documentation and comments, enhancing clarity and maintainability. Overall, the system is designed for real-time monitoring and control of motor movements based on sensor inputs, showcasing effective use of C language and STM32Cube HAL for embedded applications. Future improvements could focus on enhancing filtering algorithms, optimizing motor control strategies, and implementing more robust error handling and calibration routines to improve reliability and performance.

        1. **Overview**

A flowchart illustrating the basic structure and flow of the main file is shown below.


    _The flowchart illustrates the initialization of hardware peripherals, the main control loop, and the integration of sensor data for motor control and feedback using the program eraser.io. The remaining flowcharts will be attached at the appendix._


                

<p id="gdcalert10" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image10.jpg). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert11">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image10.jpg "image_tooltip")



                    Figure 10: Flowchart of main.c

4. **Mathematical and Physical Modeling**
    12. **Modeling to Interpret Sensor Data**

In our soft robotic tentacle project, we implemented mathematical modeling techniques to interpret sensor data, especially from the FSR and IMU sensors.

        2. **Force-Sensing Resistor (FSR)**

The FSRs were used to detect the force exerted by the gripper. The main modeling technique used was to map the analog voltage readings from the FSRs to force levels. This was achieved using the map() function in the FSR controller (fsr controller.c). The function scaled and mapped the FSR readings to a desired output range, allowing the gripper to respond to varying force levels. The goal was to ensure that the gripper could adjust its grip strength based on the user’s input via the FSRs. Challenges were encountered with noise in the FSR readings, which affected the accuracy of force detection. To improve this, we implemented a low-pass filter using the apply low pass filter() function to smooth out the FSR output.


Future improvements could focus on refining calibration techniques and reducing noise interference to enhance the accuracy of force detection. Advanced algorithms for force control could also be explored to achieve more sophisticated gripping capabilities.

        3. **IMU (BNO055)**

The BNO055 IMU sensor was used to monitor the orientation of the robotic tentacle. Mathematical modeling involved using Euler angles provided by the sensor to adjust the movement of the tentacle. A basic moving average filter was applied to the Euler angles to smooth out noise and provide more stable orientation data. This filtered data was then used to control the DC motors through the motor driver module (Motor Driver.c), adjusting the speed and direction of the tentacle based on the user’s hand movements.


Challenges were faced with maintaining consistent sensor calibration and occasional communication issues, which affected the accuracy of orientation feedback. Future improvements could focus on refining sensor calibration routines and optimizing communication protocols to enhance the reliability and accuracy of orientation data.

    13. **Calculations for Dynamic Behaviors**

Calculations for dynamic behaviors were performed to achieve precise actuation of the robotic tentacle.

        4. **Motor Control**

In the motor driver module (Motor Driver.c), calculations were performed to control the speed and direction of DC motors using PWM signals. The main calculations involved setting motor duty cycles based on the desired speed, which was influenced by the input from the IMU sensor. PID control was initially planned to be implemented using motor encoders for position feedback; however, due to hardware issues with the encoders, this was not achieved.


Future improvements could focus on resolving the encoder issues to enable PID control, which would enhance the precision and repeatability of motor movements.

    14. **Processing Sensor Data**

Processing of sensor data was crucial for the overall functionality of the robotic tentacle.

        5. **FSR Sensor Data**

The FSR controller (fsr controller.c) processed analog sensor data from the FSRs. This involved sampling and averaging ADC readings to provide stable inputs for the FSRs. The get averaged adc value() function was used to achieve this. Additionally, a low-pass filter was applied to the FSR readings using the apply low pass filter() function to ensure precise force detection.

        6. **IMU Sensor Data**

The BNO055 IMU sensor data, including orientation and system status, was read and processed in the BNO055 sensor integration module (bno055.c). Functions were implemented to set sensor operation modes, read sensor data, perform sensor calibration, and manage sensor communication. The data was then used to adjust the movement of the tentacle to maintain the correct orientation relative to the user’s hand movements.


Future improvements could focus on enhancing the filtering algorithms for the IMU sensor data to achieve more accurate and stable orientation feedback.

5. **Appendix**
    15. **Code Listing**

A full code listing is provided in a ZIP file with our STM32CubeIDE project. The zip file contains the project created in the CubeIDE, and it includes our .ioc that sets up our STM32F411CEU6 for our peripherals and desired clock cycle. Also included in this project are all the source and header files discussed in section 3.

    16. **Circuit Schematics**



<p id="gdcalert11" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image11.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert12">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image11.png "image_tooltip")





<p id="gdcalert12" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image12.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert13">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image12.png "image_tooltip")


        7. **12V-5V Buck Switch Voltage Drop Calculations**
* V<sub>drop </sub>= 12V - 5V = 7V
* Ploss = Vout × Iout = 5V × 2A = 10W
* Trise = Ploss × RJB
* T<sub>rise </sub>= 10W × 99.29<sup>◦</sup>C/W = 892.9<sup>◦</sup>C
        8. **5-3.3V LDO Regulator Drop Calculations**
* V<sub>drop </sub>= 5V - 3.3V = 1.7V
* P<sub>loss </sub>= V<sub>out </sub>× I<sub>out </sub>= 1.7V × 0.160A = 0.272W
* Trise = Ploss × RJB
* T<sub>rise </sub>= 0.272W × 100<sup>◦</sup>C/W = 27.2<sup>◦</sup>C
        9. **Oscillator Calculations**
* CL = 2 × CL - 2 × Cstray
* C<sub>L </sub>= 2 × 6pF - 2 × 3pF
* C<sub>L </sub>= 6pF
        10. **Motor Driver Calculations**
* V<sub>M </sub>= 4.5 - 13.5V
* V<sub>CC </sub>= 2.7 - 5.5V
* I<sub>OUT/ch</sub>: 1A
* Temp = 20 - 85<sup>◦</sup>C
    17. **Bill of Materials**

**Part No.	Component	Type	Quantity	Supplier	Supplier Link**



1. C7, C9	CAP, 1uF	3	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/tdk-corporation/C4532X7R1C336M250KC/1923413</span>
2. C8, C10, C12	CAP, 10uF	4	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/cal-chip-electronics-inc/GMC43X7R106K25NT/18151083</span>

        ```
RES, 10K
RES, 5.1K
RES, 10
RES, 300K
RES, 100K
MCU
USB
MOT DRIVER
JST, 2 PIN
RES, 1K
LED, RED
LED, BLUE
CAP, 0.1uF
CAP, 16pF (15)
MOT PFET
JST, 4 PIN
JST, 3 PIN
JST, 20 PIN
8MHZ OSC
EVP SWITCH
```


1. R7, R12, R9, R106	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/stackpole-electronics-inc/RMCF2010FT10K0/1758376</span>
2. R4, R82	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/koa-speer-electronics-inc/RK73B2HTTE512J/10393926</span>
3. R13, R162	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/vishay-dale/CRCW201010R0FKEF/1173910</span>
4. R51	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/vishay-dale/CRCW2010300KJNEF/1173894</span>
5. R1, R2, R63	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/te-connectivity-passive-product/CRGCQ2010F100K/8576558</span>

	91	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/stmicroelectronics/stm32f411ret6tr/7313108</span>

	101	<span style="text-decoration:underline;">https://www.digikey.com/en/models/4312191</span>

	111	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/toshiba-semiconductor-and-storage/TB6612FNG-C-8-EL/1730070?s</span>=

	122	<span style="text-decoration:underline;">https://www.digikey.com/en/models/2241777</span>

	13 R31	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/koa-speer-electronics-inc/RK73B2HTTE102J/10393884</span>

	141	<span style="text-decoration:underline;">https://www.digikey.com/en/models/14555739</span>

	151	<span style="text-decoration:underline;">https://www.digikey.com/en/models/4489933</span>



1. C11, C16, C13	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/cal-chip-electronics-inc/CHV1812N500104MXT/22238716</span>
2. C14, C152	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/knowles-syfer/1812Y3K00150JCT/6475626</span>

	181	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/diodes-incorporated/DMG3415UFY4Q-7/5970445</span>

	196	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/jst-sales-america-inc/B4B-PH-SM4-TB/926643</span>

	204	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/jst-sales-america-inc/BM03B-XASS-TF/1634764</span>

	211	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/sullins-connector-solutions/NPPC102KFMS-RC/776178</span>

	221	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/ecs-inc/ECS-80-18-30-JGN-TR/5875530</span>

	231	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/panasonic-electronic-components/EVP-ASAC1A/4930557?s=N4IgTC</span>


```
12V PFET
ZENER DIODE
BUCK SWITCH
CAP, 22uF
Inductor, 6.8mH
0.47uF
LDO 5-3.3V
CAP, 4.7uF
```


	251	<span style="text-decoration:underline;">https://www.digikey.com/en/models/3770033</span>

	261	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/toshiba-semiconductor-and-storage/cmz15-te12l-q-m/7809461</span>

	271	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/analog-devices-inc/adp2302ardz-5-0-r7/2606527</span>

	28 C2, C52	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/yageo/CC1812JKNPOEBN220/5884816</span>

	291	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/tdk-corporation/mlz2012n6r8lt000/2523499</span>

	30 C3, C42	<span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/tdk-corporation/C4532X7R2E474K230KA/789693</span>


        311 <span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/diodes-incorporated/AP7315Q-33W5-7/10294930?s=N4IgTCBcDaIII</span>A 3 C61 <span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/kemet/C1812C475M5RAC7800/2235866</span>



1. BN0055 IMU	1
2. FSR	2

	37	MOTORS	2


                                <span style="text-decoration:underline;">https://www.digikey.com/en/products/detail/adafruit-industries-llc/2472/5699182</span>

	32	SERVO	2	<span style="text-decoration:underline;">https://www.amazon.com/Dorhea-Arduino-Helicopter-Airplane-Walking/dp/B07Q6JGWNV/ref=sr_1_7?sr=8-7</span>



1. Glove Pair	1	<span style="text-decoration:underline;">https://www.amazon.com/TRENDOUX-Winter-Texting-Smartphone-Driving/dp/B07JYJM6JT/ref=sr_1_5?sr=8-5</span>
2. Wires	1	<span style="text-decoration:underline;">https://www.amazon.com/Elegoo-EL-CP-004-Multicolored-Breadboard-arduino/dp/B01EV70C78/ref=sr_1_3?sr=8</span>-

	24	XT30PW-M	1	[https://www.amazon.com/Amass-XT30PW-Upgrade-Connectors-Battery/dp/B099F2PXYN/ref=sr_1_1?sr=8-1](https://www.amazon.com/Amass-XT30PW-Upgrade-Connectors-Battery/dp/B099F2PXYN/ref=sr_1_1?sr=8-1)



    18. **Flowcharts**

                

<p id="gdcalert13" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image13.jpg). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert14">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image13.jpg "image_tooltip")



                Figure 11: Flowchart of motor driver.c




<p id="gdcalert14" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image14.jpg). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert15">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image14.jpg "image_tooltip")



                Figure 12: Flowchart of fsr controller.c



<p id="gdcalert15" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image15.jpg). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert16">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image15.jpg "image_tooltip")



                    Figure 13: Flowchart of bno055.c


        

<p id="gdcalert16" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image16.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert17">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image16.png "image_tooltip")



        Figure 14: Flowchart of receiver.c
