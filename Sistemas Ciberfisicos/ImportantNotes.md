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