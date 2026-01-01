FreeRTOS Project with Multiple Tasks
Objective

In this project, we extended the example from Chapter 4 by adding multiple tasks to control LEDs via the RP2040 microcontroller. We added 8 LEDs and 8 corresponding tasks, each with a different priority. This project aims to demonstrate task and resource management (like LEDs) under FreeRTOS and to observe the limitations and performance of the RP2040 when a large number of tasks are created.

Key Features:

Creation of 8 tasks associated with 8 LEDs (from LED1 to LED8).

Each task has a different priority to simulate varying workloads.

Monitoring of the number of tasks and execution statistics at each cycle.

Testing the RP2040's capability to handle multiple concurrent tasks.

Code Description
Code Structure

The code is designed around FreeRTOS to run multiple tasks concurrently. Each task is linked to a specific LED and has a defined priority.

Initialization Code

Task Priorities:
Each task has an increasing priority. The base TASK_PRIORITY is set to (tskIDLE_PRIORITY + 1UL), and each subsequent task increases the priority by 1 (TASK_PRIORITY + n).

LED and Task Creation:
Each LED is mapped to a separate task (worker1, worker2, ... worker8), each responsible for blinking the associated LED.

Statistics Management:
Task statistics and dynamic memory statistics are printed every 3 seconds to monitor performance.
Code Operation

Tasks associated with each LED:
Each LED (LED1 to LED8) is controlled by a separate FreeRTOS task. The priorities of the tasks vary, allowing the simulation of different workload conditions for each task. For example, worker1 has the lowest priority, while worker8 has the highest priority.

Monitoring Performance Statistics:
The runTimeStats function regularly prints statistics about the tasks running, including the number of tasks, their priority, memory usage, and the stack state of each task.

Testing RP2040's Capacity:
This program allows testing the RP2040's ability to run multiple tasks simultaneously. The number of tasks that can be created depends on the available resources on the microcontroller. You can observe the output in the terminal to check the number of tasks created and analyze whether the RP2040 has reached its limit.

Adding More Tasks and Testing

To add even more tasks, simply create new instances of BlinkAgent (or any other agent you prefer) and assign them a priority. You can easily extend this model to add more LEDs and tasks.

Conclusion

This project demonstrates how to use FreeRTOS to manage multiple tasks on the RP2040 microcontroller, particularly in a resource-constrained environment. By increasing the number of tasks and controlling multiple peripherals (LEDs), you can test the task and resource management capabilities of the RP2040.

Limitations

The number of tasks that can be created depends on the available memory on the RP2040. If you hit the memory limit, you may need to adjust stack sizes or optimize the code.
