---
layout: essay
type: essay
title: Embedded Systems and Their Applications
# All dates must be YYYY-MM-DD format!
date: 2018-10-09
labels:
  - RTOS
  - Linux
  - Android
---

## Introduction
Embedded Operating Systems are computer hardware systems that are designed attached to and controlling a function or entire machine. More specifically, an embedded system will be digital hardware programmed to act as a controller for specific functions or to control an entire other system. Examples of embedded systems can be found in engine control units in automobiles, mp3 players, coffee machines, and just about any other modern day device that contains a digital system. This paper will begin with an explanation of how embedded systems work as well as the history of implementing embedded systems. The next section will discuss how popular embedded systems work and applications of them, specifically Raspberry Pi and Arduino units. The following section will discuss the following RTOS (4.1): Apache MyNewt, ChibiOS/RT, Contiki, RIOT, RTLinux, VxWorks, and Zephyr. The final section will be a conclusion. [1]  

## Embedded Systems and Their Applications
An embedded system is computer hardware embedded into a larger system. An embedded system can either be part of the system or independent of the associated system. Microprocessors installed as embedded systems allow devices and systems to have a smaller, cheaper, digital way of controlling functions that a system must perform. Embedded systems are comprised of 3 main components: hardware, application software, and an RTOS that that controls the scheduling of task performance to ensure that certain functions are completed when required in real time. An embedded system can be defined as “a Microcontroller based, software driven, reliable, real-time control system.” Embedded systems perform repeated tasks and only perform their specialized function. For example, printer will only perform a specific function and will not perform any other function other than the printer was designed to do. [1]-[3]

The earliest embedded system recognized is the guidance computer that was used in the Apollo guidance computer designed in 1965 by MIT and was considered a major risk at the time of its implementation. The first mass produced embedded system was the Autonetics D-17 guidance computer for the Minuteman missile which featured a hard disk for memory and was created using transistor logic. Embedded systems were not commercialized until the PDP-8, a minicomputer developed by the Digital Equipment Corporation. The minicomputer was considered “low cost” for the time and was the best-selling computer in history when it was released. 1969 featured the first embedded system in a car in the Volkswagen 1600 which controlled the fuel injection in the car’s engine. Two years later Intel released the Intel 4004, which was the first 4-bit processor that was designed to be used in calculators which led to competitor Motorola to release the MC6800, the worlds first 8-bit processor, in 1974. Embedded system design continued in the early 1980s and optimized for speed and memory size for microprocessors. As the decades passed, embedded systems became a central component powering many devices such as printers, PDAs, and have become commonplace in nearly all automobiles. [3]-[5]   

Raspberry Pi is a miniature computer SOC (4.2) that is about the size of a credit card that was designed to be low cost and fully programmable. It was initially created to be a platform to educate younger children about computer programming and to encourage them to pursue the field later in life. The device released featuring an ARM microprocessor that runs at 700 MHz along with a GPU capable of 1080p output to a display. The device also features a set of pins that can interface with external devices to function as a microcontroller. Raspberry Pi is designed to use the Linux OS due to its open source nature, simplicity, and low memory overhead. An SD card is required to serve as a source of flash memory because it does not have any onboard flash storage.  	The low cost, customizability, and computing capability have led to Raspberry Pi becoming popular for projects where programmable controllers are necessary for various applications. Some popular projects include making servers for wireless printers, acting as a controller in various robotics projects, and even emulating older generation game consoles. Simple programs can be written in any language supported by the Linux OS and signals can be sent to a device being controlled via the GPIO (4.3) pins located on the Raspberry Pi. This allows the Raspberry Pi to be modified to control digital components like motor control boards and LEDs. Raspberry Pi packs a relatively large amount of computing power into a small device with endless programming capabilities and is the modern version of a digital Lego set. [6]-[8]

Arduino is an open source hardware programmable microcontroller and differs from the Raspberry Pi because it does not contain an entire SOC. Arduino is designed to be programmed and run a single designated program. The purpose of the device is to interface with sensors and externally connected devices meaning that it has been engineered with that in mind. It comes set up to interpret a wide range of input sensor data out of the box while the Raspberry Pi requires programmed software to effectively interface with other devices. The base Arduino model is called the Uno and the highest end model is called the Yun. There are many other models in between but each operate in a similar fashion while only differing in the power capability and interface ports (such as networking capabilities). Arduino Uno features an 8-bit AVR microcontroller, 32KB of onboard flash memory, Digital and Analog I/O pins, and USB ports. It is programmed using an included IDE software to write code in C/C++ which is uploaded to the board via a USB cable. Arduino can be programmed to serve many functions as a microcontroller and is used mainly for projects requiring controlling of physical components such as robotic wheels, drone propellers, and lighting/displays. [9], [10]

Real Time Operating Systems are used to control devices dedicated to a specific application such as medical equipment, industrial control systems, or display systems. An RTOS uses a multithreaded structure to manage tasks and schedule task execution. This is achieved through careful design and implementation of scheduling algorithms to ensure that functions are executed in a predictable time. 

There are many choices for different RTOSs to program onto an embedded system for handling the way signals are prioritized during operation. Apache MyNewt handles the scheduling of different tasks by labeling threads as either running, ready to run, or sleeping. Each task has a priority value associated with it between 0 and 255 which the scheduler uses to determine which order the have threads run in. The algorithm the scheduler uses is very simple and just takes the task with the highest priority (lowest numerical value) and sets it to run while maintaining other tasks that are “ready to run” in a linked list sorted by priority order. [2] 

ChibiOS/RT handles scheduling by have each task have a fixed priority numeric value and using it to run threads in a similar fashion to Apache MyNewt. ChibiOS/RT uses an API for other modules to implement synchronization primitives. Synchronization can be achieved via counting and binary semaphores (4.4) and mutexes (4.5). The ready list structure is a bidirectional linked list sorted by priority, the lowest priority thread is a special thread called the “idle thread” which only runs when no other thread is running or ready. [2] 

Contiki runs code in one of two contexts: cooperative or preemptive. Cooperative code will run sequentially as it is scheduled, and preemptive code will stop cooperative code and run. Each process has a process control block containing a pointer to the next process in the active process list, a name for the process, a pointer to the process thread, and status flags used by the scheduler. In Contiki, processes are run when they receive an event which are categorized as synchronous and asynchronous events. Asynchronous events are delivered directly to the receiving process and synchronous events will be put in the event queue and delivered when it waits for its turn. [13]

RIOT-OS operates by having two different ways that context switches can occur: preemptively or voluntarily. Preemptive switches are interrupts and will take priority over running threads. Voluntary contexts switches will only occur if a thread either yields or sleeps to allow another thread to run. RIOT-OS does not have a timer that periodically causes threads to switch and emulate concurrent execution. Synchronization is achieved through implementation of mutexes. RIOT-OS was designed to meet the requirement of devices to be connected to the internet via embedded systems and to maintain a low memory footprint. [14]

RTLinux (real time Linux) differs from normal Linux in that it is geared toward real time applications by handling scheduling differently. The normal Linux kernel prevents any one thread from monopolizing its processor all the time regardless of priority via timed context switches. The Real Time Linux kernel will always run the higher priority thread via executing preemptively. Preemptive threads can run forever if they are not blocked by a synchronization resource or preempted by a thread of equal or higher priority. RTLinux uses the First-In-First-Out method for scheduling threads with the same priority and handles processes in the order they are received. [15]

VxWorks uses a numeric priority value associated with each process and the Round Robin method of scheduling. Along with the normal method of priority scheduling, each process is given a time slice in which to run. When the time slice expires, the processor switches to a different thread and the new thread executes until it either finishes or its time expires. The round robin method allows for multiple threads to progress in a given time period rather than to wait until a process completes before allowing another to process. [16]

The Zephyr kernel is a designed for resource constrained systems and is customizable to meet the size requirements of the situation it is applied in. Zephyr’s scheduler works very similar to the VxWorks scheduler in that it applies the Round Robin method with one large notable difference. Zephyr has cooperative threads operate in time slices but also gives preemptive threads a time slice that when expiring will check to see if the current thread is preemptable and, if so, will yield the thread to another with the same priority. This prevents a long running high priority thread from locking out other threads of the same priority level. [17]


## Conclusion
Embedded systems have become ubiquitous in modern technology with the rising demand for devices to support internet connectivity and wireless features. These conveniences of modern living are only made possible by the creation and distribution of customizable hardware and real time operating systems. The scheduling systems designed by real time operating systems allow a computer system to make calculations and execute functions within given time constraints to make reliance on digital hardware feasible. Embedded operating systems are the building blocks to innovation in the modern day.


## References
[1]	"Embedded Systems Overview", www.tutorialspoint.com, 2018. [Online]. Available: https://www.tutorialspoint.com/embedded_systems/es_overview.htm. [Accessed: 12- Oct- 2018].

[2]	"ChibiOS free embedded RTOS - Chibios:book:start", Chibios.org, 2018. [Online]. Available: http://www.chibios.org/dokuwiki/doku.php?id=chibios:book:start. [Accessed: 12- Oct- 2018].

[3]	"Embedded system", En.wikipedia.org, 2018. [Online]. Available: https://en.wikipedia.org/wiki/Embedded_system. [Accessed: 11- Oct- 2018].

[4]	"Embedded In Our Society: A History Of Embedded Operating Systems", Hughes Systique Corp., 2018. [Online]. Available: https://hsc.com/Blog/Embedded-In-Our-Society-A-History-Of-Embedded-Operating-Systems-1. [Accessed: 11- Oct- 2018].

[5]	H. Garden, C. Hardware and H. Basics, "How the Raspberry Pi Works", HowStuffWorks, 2018. [Online]. Available: https://computer.howstuffworks.com/raspberry-pi.htm. [Accessed: 11- Oct- 2018].

[6]	"20 Awesome Uses for a Raspberry Pi", MakeUseOf, 2018. [Online]. Available: https://www.makeuseof.com/tag/different-uses-raspberry-pi/. [Accessed: 12- Oct- 2018].


[7]	"Raspberry Pi Hardware Guide | Raspberry Pi Learning Resources", Raspberrypi.org, 2018. [Online]. Available: https://www.raspberrypi.org/learning/hardware-guide/. [Accessed: 12- Oct- 2018].

[8]	"GPIO - Raspberry Pi Documentation", Raspberrypi.org, 2018. [Online]. Available: https://www.raspberrypi.org/documentation/usage/gpio/. [Accessed: 12- Oct- 2018]. aspberrypi.org. (2018). GPIO - Raspberry Pi Documentation. [online] Available at: https://www.raspberrypi.org/documentation/usage/gpio/ [Accessed 12 Oct. 2018].

[9]	"The Absolute Beginner's Guide to Arduino", Forefront.io, 2018. [Online]. Available: http://forefront.io/a/beginners-guide-to-arduino/. [Accessed: 12- Oct- 2018].

[10]	"Arduino vs. Raspberry Pi: Mortal Enemies, Or Best Friends? Take A Look! | Digital Trends", Digital Trends, 2018. [Online]. Available: https://www.digitaltrends.com/computing/arduino-vs-raspberry-pi/. [Accessed: 12- Oct- 2018].

[11]	C. Walls, "Tasks and scheduling", Embedded, 2018. [Online]. Available: https://www.embedded.com/design/operating-systems/4443042/Tasks-and-scheduling. [Accessed: 12- Oct- 2018].

[12]	"Mynewt Documentation — Apache Mynewt 1.3.0 documentation", Mynewt.apache.org, 2018. [Online]. Available: https://mynewt.apache.org/latest/. [Accessed: 12- Oct- 2018].


[13]	GitHub. (2018). contiki-os/contiki. [online] Available at: https://github.com/contiki-os/contiki/wiki/Processes [Accessed 12 Oct. 2018].
 
[14]	"RIOT Documentation", Riot-os.org, 2018. [Online]. Available: https://riot-os.org/api/index.html#riot-in-a-nutshell. [Accessed: 12- Oct- 2018].

[15]	"Comparing real-time scheduling on the Linux kernel and an RTOS", Embedded, 2018. [Online]. Available: https://www.embedded.com/design/operating-systems/4371651/Comparing-the-real-time-scheduling-policies-of-the-Linux-kernel-and-an-RTOS-. [Accessed: 12- Oct- 2018].

[16]	T. Agarwal, "Real Time Operating System RTOS in Vxworks", Buy Electronics & Electrical Projects in the United States, 2018. [Online]. Available: https://www.efxkits.us/real-time-operating-systems-rtos-in-vxworks/. [Accessed: 12- Oct- 2018].

[17]	"Scheduling — Zephyr Project Documentation", Docs.zephyrproject.org, 2018. [Online]. Available: https://docs.zephyrproject.org/1.6.0/kernel_v2/threads/scheduling.html. [Accessed: 12- Oct- 2018].
