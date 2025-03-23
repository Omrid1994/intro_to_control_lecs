# Chapter 1: The Challenge of Control

What is control theory all about? Consider a dynamical system with an input $u(t)\in\mathbb{R}^m$ and an output $y(t)\in\mathbb{R}^p$. Roughly speaking, the input is what we can control and the output is what we can measure. For example, in a model of a moving vehicle the input may be the pressures on the gas pedal and the brakes pedal, whereas the output may be the speed of the vehicle. The system to be controlled is called the plant.  

Our goal is to regulate the plant's output to some desired behavior. For example, in the model of a vehicle we may wish to 
regulate the vehicle's speed $y(t)$ to some desired speed profile $r(t)$.
Control theory allows to systematically design and analyze an automatic controller that changes the plant's input in an attempt to make the error $e(t):=r(t)-y(t)$ small (in a suitable sense). This should hold even under various disturbances. Typically, the controller is connected in a  feedback form: the controller input is $e$, and the controller output is fed to the plant's input. The result is a feedback loop that also takes into account the existence of disturbances, see {numref}`fig-closed-loop`. 

Control theory plays a crucial role in  robotics, manufacturing processes, aerospace systems, electrical and electronics engineering, chemical engineering, and more.  
 In  our  era of autonomous systems, such as self-driving cars, drones, and ships, control theory is 
 an indispensable tool  for  designing systems that are efficient, reliable, and resilient to disturbances.

```{figure} images/closed_loop1.png
---
width: 70%
name: fig-closed-loop
---
Feedback connection of a plant and a controller. $d$ denotes a disturbance signal.


