# Introduction

A cyber-physical system is defined as a physical system whose operations are monitored, coordinated, controlled and operated by a computing core.

A real-time system is system whose progression is defined in terms of timeliness based on the requirements of the environment, and whose actions need to be synchronized with the same environment.

There are 3 types of RT systems:
- Soft RT - Timing failures must be avoided
- Hard RT - Occasional timing failures must be avoided, but can be accepted
- Mission-Critical RT - Occasional timing failures must be avoided, and must be handled with exceptions

Deadlines must be met both during normal operation and faulty operation

# Paradigms

## Temporal Specifications

Definitions:
- Response time : Interval between the input event and the first output event
  1. Maximum Response time - Measures how much a system can manage a control process
  2. Minimum Response time - Measures the variance at which a computer responds
- Timed action : The execution time of an action that started in a moment $t_A$ within an interval $T_A$
- Termination time : Time measured from request to termination event
- Timing errors (Jitter) : Uncertainty of the termination instant of some action, can be presented in the form of
  1. Variance regarding a value
  2. Imprecision in the positioning of the termination event
- Timing of events
  1. Time-Triggered approach
  2. Event-Triggered approach

Event Arrival Classification
- Distribution
  1. Aperiodic - No bounds regarding inter-arrival time of events
  2. Periodic - Events occur periodically
  3. Sporadic - Events occur sporadically but within some bounds
- Utilization Factor - Measurement of the percentage of useful work time of a resource
- Burst
  1. Burst Period - Minimum delay between bursts (with a know lower bound)
  2. Burst Length - Maximum amount of information in a burst

## Scheduling

Scheduling defines how a certain resource is shared across different tasks, given a certain policy, the main goal will be for all time sensitive tasks for meet their deadlines

Real-time scheduling is divided into multiple branches
- Soft
- Hard
  - Static - Scheduling according to a predefined plan
    1. Performed offline
    2. Requires Periodic/Sporadic Distributions
  - Dynamic - Scheduling according to a plan computed in runtime
    1. Rate Monotonic
     - Preemptive
     - Priority inversely proportional to period
    2. Deadline Monotonic
     - Preemptive
     - Priority inversely proportional to deadline
    3. Earliest-Deadline-First
     - Preemptive
     - Priority proportional to deadline
    4. Least-Laxity
     - Preemptive
     - Priority inversely proportional to laxity
    5. First-Come-Served

Priority
- Fixed - Priority unchanging at runtime
- Dynamic - Priority may change at runtime

This can be even subdivided into:
- Preemptive - Task can be interrupted during runtime, normally by a higher priority task
- Non Preemptive - Task can't interrupted during runtime, until completion 

To calculate schedules we can use:
- Centralized - Scheduling decisions are done by one entity
- Distributed - Scheduling decisions are done by different nodes

Testing:
- Sufficient - Passing means it is schedulable, failing means nothing
- Necessary - Failing means it isn't schedulable, passing means nothing
- Exact - Passing means it is schedulable, failing means it isn't schedulable

## Priority Inversion

Priority inversion is a problem characteristic to some scheduling algorithms in which:
- Low priority task gets lock on resource
- Medium priority task preempts low priority task, without it releasing the lock
- High priority task preempted medium priority, and tries to get lock on resource
- High priority is blocked because it can't get lock

Definitions
- Blocking time - Maximum time a task can be blocked by another with lower priority
- Interference time - Maximum time a task can be suspended by another with higher priority

Solution protocols
- Original Ceiling Priority Protocol
  - Each task has a static default priority
  - Each resource has a static ceiling priority, which is equivalent to the maximum priority of all tasks using the resource
  - Each task has a dynamic priority which is the maximum of its own priority and any it inherits from higher blocking-priority tasks
- Immediate Ceiling Priority Protocol
  - Each task has a static default priority
  - Each resource has a static ceiling priority, which is equivalent to the maximum priority of all tasks using the resource
  - Each task has a dynamic priority which is the maximum of its own priority and the ceiling of any resources it has locked


## Timing Failure Detection

Timing failure occurs when an timed action that is supposed to end in $t_A$ ends after $t_A$.

To this effect detection of timing failures should be:
- Timely - Detect failure in bound time
- Complete - Detecting all timing failures as timing failures
- Accurate - Not detecting timely actions as timing failures

## Entity and Representatives

The relationship between the elements of the environment (RTe RealTime entity) and their computational counterparts (RTr RealTime representative), is essential to represent CPS's.

Certain characteristics need to be maintained:
- Temporal accuracy - Defines a bound in time at which RTe and RTr need to be the same
- Temporal validity - Defines an interval at which RTr is correct  


## Time and Clocks

Global time - Time abstraction based on time values from clocks in the system

Absolute time - Time abstraction based on time values from a common time standard (UTC)

Clocks are defined based on 3 values:
- Precision : Difference between 2 clock values 
- Accuracy : Difference between 1 clock and the real time
- Granularity  : Maximum clock increment

Clock drift, is an accuracy in which a clocks value drifts at a certain rate from the real time and therefore needs resynchronization every so often.

Clock synchronization can be made in 2 ways:
- Internal - Based on clocks inside the network, and therefore only assures precision
- External - Based on clocks outside the network assuring precision and accuracy

and can be dependant on 2 methods
- Software-Based - Synchronized through messages, while inexpensive it is harder to achieve high clock precision
- Hardware-Based - Synchronized through direct communication, while expensive the precision is very high

## Input/Output

There are 3 main techniques for observation or input:
- Sampling - Used to observe continuos entities
- Latching - Used to observe discontinuous entities
- Interrupt - Used to observe sporadic entities

There are 3 main techniques for actuation or output:
- Immediate - Actuation as soon as issued
- Deferred - Invoked to be issued after a specified delay
- Periodic - Invoked to be cyclicly repeated, with period T

# Models of CPS's

A control system, is the part of a CPS which is responsible for providing the desired system response.

There are 2 main ways of doing control:
- Open loop - Uses a controller and an actuator to obtain the desired response
- Closed loop - Uses a feedback signal from the actuator to compare the desired output with the measured output. The goal will be to minimize Error = Desired output - Measured Output

The design and analysis of CPS's requires quantitative models describing the dynamic behavior of the model, to this effect there needs to be made a distinction between 2 types of models:
- Continuous 
- Discrete


## Continuous Models

Continuous models require Differential equations to describe themselfs.

This is caused becuase these systems are usually physical in nature, and physics is represented by differential equations.

These equations are usually obtained from physical laws.

Representation:
- State : Smallest set of variables, which can be used to describe the system for $t>T_0$
- State Vector $x(t)$: Vector of derivatives of n state variables at time t
- State Space : n-dimensional space whose coordinates axes relate to the state variables
- State Trajectory : Path at which $x(t)$ evolves
- Transfer Function : Function able to describe the entire the state of a system given input. Function that models the system when given input. Usually obtained using a laplace transform over the differential equations

These systems usually can be categorized:
- Causality
  - Casual - Output depends only on the present and the past input
  - Strictly Causal - Output depends only on the past input
- Memoryless
  - System with memory - Output depends on current, past ant future (if not causal) input
  - System without memory - Output depends on current input
- Linearity
  - Satisfies superposition
  - Satisfies Homogeneity
- Time-Invariance - A systems output is invariant of time
- Stability - A system is stable if it has Bound-Input Bound-Output, if for all values of input there is a defined output

## Discrete Models

In discrete systems we are trying to convert the continuous data we are given from the real world into discrete values which computers work with

To do this we need to convert signals analog systems into digital and the other way around:
- Analog -(Sample)> Sampled Data -(Hold)> Quantized -(Quantize and Encode)> Digital
- Digital -(Decode)> Sampled Data -(Hold)> Quantized -(Filter)> Analog

To do this we use 2 components:
- DAC - Digital Analog Converter
- ADC - Analog Digital Converter

Controllers usually depends on 3 values to create new output:
- Current error value
- Past error values
- Past controller outputs

Just like laplace transforms can be used in continuous systems to obtain transfer function, in discrete systems we can use Z transform to the same effect, but instead of getting them in s domain we use Z domain, we given they are interchangeable between them means we can convert continuous systems in discrete systems.

This transition will lose some of the meaning given to continuous/discrete system.

# PID

The PID controller is an Closed Loop controller in which we use 3 terms to obtain new controls.

The 3 terms are combined by:
$$u(t)=K_pe(t) + K_i\int^t_0 + K_d\frac{de(t)}{dt}$$

This $u(t)$ value is then passed to the actuator to be used on the system.

The terms influence the output:
- P - Proportional, the present
- I - Integral, the past
- D - Derivative, the future

Higher P -> More overshoot, faster response and steady-state != 0

Higher I -> Smaller Overshoot, slower response and steady-state = 0

Higher D -> Smaller Overshoot, faster response and steady-state != 0

In order to optimize the values we must:
- Set $K_p,K_i,K_d$ to zero
- Increase $K_p$ until the values oscillate steadily, and take note of the current $K_p$ and oscillation period
- Design the controller based on those values

# Control Systems

Microcontroller is a small computer in a single integrated board, which is normally used to control CPS's

Microprocessor is the CPU for the microcontroller, the defining characteristics of a microprocessor are:
- Energy Usage - Needs to be small
- Memory - Needs to store: program, stack, data
- Clock Frequency - Several hundred MHz
- I/O pins - Needs a large variety and number of I/O pins
- Internal Functions


There are 2 implementations of I/O Pins
   - Port I/O - Devices are registered to ports
      - are defined in a separate address space
      - use different methods to interact with them
      - these methods can be dependant on the MCU
      - requires special hardware to protect
      - reads and writes can be bound to operation triggers
   - Memory Mapped I/O - Devices are registered to regular address space 
      - use normal memory management methods 
      - use memory protections mechanisms to be protected
      - always use normal memory management methods, therefore aren't dependant on MCU
      - Allows for more flexibility

GPIO are the general design of the input/output device, they usually represent a single bit.

## Arduino

Digital inputs - Can be HIGH(5VDC) or LOW(0VDC)

Analog inputs - Can be range of numbers from 0 to 1023

Programs are called sketches, and need to have 2 functions:
- setup: runs first and once
- loop: runs over and over

Pulse-Width Modulation: a technique in which we change the values of the output for a pin at a certain frequency with the intention of changing the average power level of the signal in that pin.
This allows for the possibility of encoding information in a transmission which is only on or off.

Duty cycle is the amount of time per pulse, in which the signal is on a HIGH/on state.


# Real-Time Operating Systems

The main differences between RealTime Os's and general use OS's are:
- Real-time requires always predictable behavior, with timing guarantees and under worst case scenario
- General use can be most of the time good behavior, with high throughput under normal behavior 

Advantages of a RealTime kernel:
- Abstracting away timing information, kernel is responsible for timing therefore allowing simpler application design
- Easier Testing - Tasks can be independent of other modules, allowing for test in isolation
- Idle time utilization - Idle task can execute while there are no other tasks being run, it can be used to perform background checks or place process into low-power mode.

Why the linux kernel isn't realtime:
- Kernel can't be preempted
- Applications run in user space
- Hardware interaction is done in the kernel

To convert linux kerne into RT we can use a patch which changes:
- Adds a RT scheduler for RT tasks, and a non RT scheduler for non RT tasks
- RT coexists with linux tasks but has a higher priority
- Events, which are traps or interrupts, cause disturbances in the execution of commands
- RTLinux has priority over events processing them before linux
- ADEOS (Adaptive Domain Environment for Operating Systems) is used for event management

ADEOS offers a virtualization layers between OS and hardware and allows events to be cascaded through domains

## Xenomai

Time values are stored in timespec structures

clockid_t is a data types used to store real-time clock, it can be used in modes:
- CLOCK_REALTIME - Represents a real-time clock
- CLOCK_MONOTONIC - Represents the time since system startup

It is possible to define scheduling approaches by providing an algorithm and attributes

To avoid starvation we should use resource reservations, or use algorithms with dynamic priorities like EDF.

Concurrency can be solved by 2 means in Xenomai
- Mutexes
- Condition variables

## FreeRTOS

Tasks have their own context and no knowledge of the scheduler, the scheduler defines its own activity and context switching

Tasks have 4 states:
- Ready - Able to execute, but not executing because of higher priority task
- Running - Actively executing
- Blocked - Waiting for temporal event
- Suspended - Only possible if suspended through API calls

Each task has a priority between 0 and MAX_priority, and tasks can change their own and other tasks priorities.

Idle task is created on boot up, and is used to free up memory of tasks that have been deleted and therefore it is essential that the idle task is not starved.

Concurrency can be solved using:
- Counting Semaphores
- Mutexes
- Binary Semaphores


# Wireless Sensor Networks

WSN are wireless networks composed by thousands of independent nodes which are used to monitor physical and environmental conditions.

Nodes must be:
- Small size and low cost
- Low energy and computational requirements
- Not require battery replacement
- Self-organizing

The network should:
- Have ad hoc deployment, therefore need nearest-neighbor communication
- No battery changes requires efficient usage of energy
- Scalable and reliable, with self-configuration and good coverage
- Data collection should be clustered or centralized(even though centralized puts more strain in some nodes)

Design Challenges:
- Heterogeneity of devices - Networks might be constituted of many different device types
- Distributed Processing - Centralized algorithms are costly, processing should be decentralized
- Real Time Computation - Computation should be done quickly given new data is always being generated
- Utilization of resources - maximize performance with lowest energy cost 

ZigBee is a type of WSN:
- Composed of 3 types of nodes
  - Coordinator - Maintains the state of the network, there is only one per network and requires more resources 
  - Router - Node that forwards messages to end devices
  - End device - Node responsible for producing data, may be asleep most of the time


# CAN and ProfiBus

## CAN

CAN or controller area network is a type of network system which is based on different nodes connecting to a BUS which is shared across all nodes to transport messages.

Instead of using 0 and 1 to represent bits CAN uses 2 signals CANHigh and CANLow, the subtraction of the values of the 2 signals is used to obtain the final value of the signal.

This is used to minimize the effect of noise upon the BUS, and it leads to having 2 output signals:
- 0 - Dominant Bit
- 1 - Recessive Bit

At any time the BUS can only have one Bit value.

The Bus is composed of 2 wires to assure tolerance to faults.

Packets have unique identifiers, which are used for bus arbitration and therefore there is no need for source/destination addresses

When sending a packet, the identifier is the firs to be transmitted if the node notices that a value put in the bus doesn't correspond to the value it reads from the bus it detects a conflict (when the node puts a recessive bit in the bus and reads a dominant bit). After a conflict is detected the bus passes from sending mode to receiving node.

This implies identifiers with more 0's in the left have higher priority, therefore smaller values of identifier have higher priority

The packets are sent in a specified form where some field are specifically left as recessive in order to allow receiver with error to ask for retransmission

The ACK bit is put to recessive by the sender, if any node receives it correctly passes it to dominant indicating to the sender that at least one node received the packet correctly.

Errors are usually solved by retransmission, errors can originate from:
- bit errors - mismatch between transmitted and received bits
- bit-stuffing errors - stream with more than 5 consecutive same value bits
- CRC error - mismatch between sent and received CRC (CRC is similar to a checksum every node calculates autonomously, if it mismatches the recessive bit is passed to dominant)
- ACK error - lack of ACK in the ACK slot
- form error - violation of frame fixed form

Moreover every 5 consecutive bits with the same value, there is a flipped bit in order to assure synchronization.


## Profibus

ProfiBus is a type of fieldbus based on a tree type topology.

There are 2 types of nodes: master and slave

Masters poll slaves for frames.

Nodes use tokens to access the bus, a the token is passed around the master nodes based on a TTRT (Target Token Rotation Time).


## TTP

Time Triggered Protocol it is similar to profibus with a master/slave dynamic.

But uses aditionally:
- FTU (Fault Tolerant Unit) - replicates nodes
- Broadcast bus
- Clock Synchronization
- Periodic message exchanges

Regarding the Bus it is:
- replicated to assure space redundancy
- duplicated broadcasts to assure time redundancy

FTU are clusters of nodes executing the same computations in order to assure fault tolerance, there are different levels of FTU:
- Class 1
  - One node per FTU
  - 2 frames per FTU, one on each bus
- Class 2
  - Two nodes per FTU
  - 2 frames per FTU, each node on one bus
- Class 3
  - Two nodes per FTU
  - 4 frames per FTU, 2 for each node on one bus
- Class 4
  - Two nodes per FTU and one shadow node, the shadow node does the same as other nodes but doesn't transmit to bus
  - 4 frames per FTU

FTU frame types:
- I-Frame
  - used for initialization
  - also used to re-sync nodes to cluster
- N-Frame
  - used for normal messages