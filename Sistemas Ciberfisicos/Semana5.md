# PID Controler

PID stands for Proportional Integral Derivative controller
It is the most used controller in industry

Controller that works based on the error of the system, combined with the actual output of the system.
It uses 3 terms :
- Proportional term
- Integral term
- Derivative term
To calucalte a new input to the system, these 3 terms take as input the $e(t)$ or the error of the system, in form of function.

During the execution of a PID it can respond with multiple types of response
- Under-damped - 
- Critical-damped - 
- Over-damped - 

There are mutiple values to define a PID
- Maximum overshoot - Maximum value which the PID overshoot the value of the command
- Settling Time - Total time the PID took to output the semi-correct value of the command (inside a band of possible correct value)
- Steady State Error - Time after the PID entered the semi-correct value band to the point in which the value is correct
- Rise Time - Time in which the system passes from previous value to try to correct to the new value


