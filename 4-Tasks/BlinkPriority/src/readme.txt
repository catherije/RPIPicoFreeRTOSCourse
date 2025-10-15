Overview
--------
This project is a FreeRTOS-based demo for the Raspberry Pi Pico.
It demonstrates how to create and manage multiple tasks to blink LEDs using FreeRTOS.
The program runs three blinking agents and periodically reports runtime and heap statistics to the serial console.

Features
--------
- Uses FreeRTOS tasks to blink LEDs asynchronously
- Demonstrates task creation, priorities, and scheduling
- Displays runtime task statistics and heap memory usage
- Designed for the Raspberry Pi Pico (RP2040)
- Modular design with external classes:
  - BlinkAgent
  - BlinkWorker
  - BlinkHeavy

File Structure
--------------
main.cpp             - Main program (this file)
BlinkAgent.h/.cpp    - Class to manage a simple LED blink task
BlinkWorker.h/.cpp   - Worker LED blinker
BlinkHeavy.h/.cpp    - High-priority, resource-intensive LED blinker
CMakeLists.txt       - Build configuration (not shown here)

How It Works
------------
1. Main Task (mainTask)
   - Creates three blink agents (BlinkAgent, BlinkWorker, BlinkHeavy)
   - Starts them with increasing priorities
   - Periodically prints system stats every 3 seconds

2. runTimeStats()
   - Collects and displays info about all running tasks:
     * Task number
     * Current and base priority
     * Stack high-water mark
     * Task name
   - Displays heap statistics

3. vLaunch()
   - Creates the main FreeRTOS task
   - Starts the scheduler

4. main()
   - Initializes USB serial
   - Waits a few seconds for the USB to settle
   - Launches the scheduler

Hardware Setup
--------------
LED #1  -> GPIO 1  (BlinkAgent)
LED #2  -> GPIO 2  (BlinkWorker)
LED #3  -> GPIO 3  (BlinkHeavy)

You can modify LED_PAD, LED1_PAD, and LED2_PAD to use different GPIO pins.

Build and Run
-------------
Requirements:
- Raspberry Pi Pico SDK
- FreeRTOS for RP2040
- CMake and GCC ARM toolchain

Steps:
1. Place the project inside your Pico SDK workspace
2. Create a build directory:
   mkdir build && cd build
   cmake ..
   make
3. Flash the .uf2 file onto your Pico
4. Open a serial monitor at 115200 baud
5. Observe LED blinking and task statistics

Example Output
--------------
GO
Starting FreeRTOS on core 0:
CATHERINE Jean
F14228823
Main task started
Number of tasks 4
Task: 1     cPri:1    bPri:1    hw:420    Blink
Task: 2     cPri:2    bPri:2    hw:380    Worker 1
Task: 3     cPri:3    bPri:3    hw:360    Worker 2
Task: 4     cPri:1    bPri:1    hw:480    MainThread
HEAP avl: 34500, blocks 10, alloc: 12, free: 3
