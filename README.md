# Objects relationships - Coding-Dojo

This repositoriy contains two coding exercises to experience the impact of composition and other techniques on objects relationships encapsulation compared to the simplistic design approach.


**Prerequisites:**
- Practical understanding of basic design principles, SOLID principles and Simple Design
- Experience with fundamental refactoring and design patterns of unit testing as in coding-dojo [Refactoring legacy code driven by tests] (https://github.com/lucaminudel/TDDwithMockObjectsAndDesignPrinciples/blob/master/TDDMicroExercises/README.md)

## Exercise 1. Simplistic design

The goal of this exercise is to experience the impact of simplistic design when new code changes are required.
In order to keep the design simplistic, 
- create direct dependencies between objects. I.e. here A -> B, concrete class A will istantiate and reference directly concrete class B instead of using interfaces or other abstractions or dependency inversions techniques;
- each feature that requires computations on the whole object graph, should be implemented in a single method that navigate the graph and compute the operation instead of introducing abstractions such as composite design pattern, visitor pattern, or any other abstraction.

The list below contains all the feature requests to be implemented. Implement one feature request at a time, without anticipating the following ones. You are encouraged to write unit tests. Every feature request should only take few minutes to implement. For every new feature request take notes of the difficulties you encountered because of the design.

**The problem:** We want to model different parts of a robot, connect them in different ways as the robot evolve, and implement some features that act on all robot parts.

1. **Left arm**
  - [x] Implement a robot left arm. 
The left arm accepts and executes a command in the form of a string. For the shake of this exercise, it's sufficient to implement just the "check" diagnostic command that writes, to the output console or to a log, the status of the arm in the form of this message: "Left arm status is ok."
  - [x] The left arm also has a max charge (in Ampere Hour or Ah) of its internal 24KV battery.
  - [x] Finally the left arm also has a current On/Off switch status.
2. **Robot bus**
  - [x] the robot bus is electricity powered.
  - [x] it has an On/Off status like the left arm.
  - [x] the left arm is connected to the robot bus and when the robot bus receive a command, the command is sent to the left arm.
3. **Right thigh**
  - [x] the right thigh is connected to the robot bus from which can receive commands 
  - [x] like the left arm it has an On/Off switch status and the max charge of the internal battery
4. **Dashboard**
  - [x] implement a function that reports the On/Off status of each part the robot as a report with with line per part that include the part name and the status
  - [x] implement a function that calculate the total cost to charge all the internal batteries; the cost for one Ah is £0.2.
5. **Right lower limb and right foot**
  - [x] add a right lower limb and a right foot and connect them to the robot bus. 
  - [x] update the the two dashboard reports accordingly.
6. **Neck and head**
  - [x] add a neck and a head and connect them to the robot bus. 
  - [x] update the the two dashboard reports accordingly
7. **Hip**
  - [x] add a hip and connect it to the robot bus. Hip has itself an On/Off status, a max charge and accepts commands as well.
  - [x] connect the arm, the thigh, the lower limb and the foot to hip. Add indentation to the On/Off status report to visually represent the tree structure.
8. **Shoulders**
  - [x] add a shoulders part and connect it to the robot bus. Shoulders part as hip has On/Off status and so on.
  - [x] connect the neck and the head to shoulders part. Use again indentation in the On/Off status report. 
9. **Trunk**
  - [x] rename robot bus to trunk.
10. **Right leg parts**
  - [x] connect right lower limb to the right thigh and the right foot to the right lower limb. Ensure report indentation reflects the new structure. Ensure commands are transmitted correctly between connected parts.
11. **Head parts**
  - [x] connect head to the neck. As before update report indentation and ensure correct commands transmission.
12. **Head parts On/Off status format change**
  - [x] if you are using boolean as current representation, change it for the neck and the head to enum, constants or flags. Or the other way round.



## Exercise 2. Target design


The goal of this exercise is to experience a different design that reduces the impact of changes to objects in the object graph and of changes to the object graph itself. In order to use a different design,
- invert the dependencies from the dashboard functions (On/Off status report and total cost to re-charge all the internal batteries) to the robot parts so that the robot parts have a dependency to the dashboard and not the opposite;
- use a common interface and if needed the adapter pattern to abstract away differences between different robot parts;
- pass the dashboard to the robot parts as a visitor in the visitor pattern; let each robot part take care of passing the dashboard to the robot parts directly composed/connected so that the responsibility of navigating the object graph moves from the dashboard functions into each robot part that compose/connects another robot part(s).

As for the previous exercise, the list below contains all the feature requests to be implemented. Implement one feature request at a time, without anticipating the following ones. You are encouraged to write unit tests. Every feature request should only take few minutes to implement. For every new feature request take notes of the difficulties you encountered because of the design.

**The problem:** We want to model different parts of a robot, compose them in different ways as the robot evolve, and have some features carried out by the composite of robot parts.

1. **Left arm**
  - [x] Implement a robot left arm. 
The left arm accepts and executes a command in the form of a string. For the shake of this exercise, it's sufficient to implement just the "check" diagnostic command that writes, to the output console or to a log, the status of the arm in the form of this message: "Left arm status is ok."
  - [x] The left arm also has a max charge (in Ampere Hour or Ah) of its internal 24KV battery.
  - [x] Finally the left arm also has a current On/Off switch status.
2. **Robot bus**
  - [x] the robot bus is electricity powered.
  - [x] it has an On/Off status like the left arm.
  - [x] the left arm is connected to the robot bus and when the robot bus receive a command, the command is sent to the left arm.
3. **Right thigh**
  - [x] the right thigh is connected to the robot bus from which can receive commands 
  - [x] like the left arm it has an On/Off switch status and the max charge of the internal battery
4. **Dashboard**
  - [x] implement a function that reports the On/Off status of each part the robot as a report with with line per part that include the part name and the status
  - [x] implement a function that calculate the total cost to charge all the internal batteries; the cost for one Ah is £0.2.
5. **Right lower limb and right foot**
  - [x] add a right lower limb and a right foot and connect them to the robot bus. 
  - [x] update the the two dashboard reports accordingly.
6. **Neck and head**
  - [x] add a neck and a head and connect them to the robot bus. 
  - [x] update the the two dashboard reports accordingly
7. **Hip**
  - [x] add a hip and connect it to the robot bus. Hip has itself an On/Off status, a max charge and accepts commands as well.
  - [x] connect the arm, the thigh, the lower limb and the foot to hip. Add indentation to the On/Off status report to visually represent the tree structure.
8. **Shoulders**
  - [x] add a shoulders part and connect it to the robot bus. Shoulders part as hip has On/Off status and so on.
  - [x] connect the neck and the head to shoulders part. Use again indentation in the On/Off status report. 
9. **Trunk**
  - [x] rename robot bus to trunk.
10. **Right leg parts**
  - [x] connect right lower limb to the right thigh and the right foot to the right lower limb. Ensure report indentation reflects the new structure. Ensure commands are transmitted correctly between connected parts.
11. **Head parts**
  - [x] connect head to the neck. As before update report indentation and ensure correct commands transmission.
12. **Head parts On/Off status format change**
  - [x] if you are using boolean as current representation, change it for the neck and the head to enum, constants or flags. Or the other way round.

## Reflections points

- xxx
- xxx
- xxx

The exercises are based on concepts covered by this post (there's no benefit in reading it before the exercise, read it after to connect the dots): http://blogs.ugidotnet.org/luKa/archive/2015/01/20/overcoming-the-one-weakness-of-oop.aspx
