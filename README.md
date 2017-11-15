# CarND-Path-Planning-Project
Ego car is able to drive across the track without any collisions nor exceeding jerks or spee limits.
A single new file was added src/spline.h (Cubic Spline interporaion implemention).
Project is partially based on the suggestions from teh classroom QA video.
   
### Prediction
This part of the code (ln. 248 - ln. 285) is responsible for environmental awareness.
Using telemetry and sensor fusion system determines if the card in front of the ego car is blocking it and if it is safe to perform lane change (either right or left).
System calculates lane for each other, non-ego car and performs projectoin of where each car will be at the end of the last plan trajectory.

### Action
This part of the code (ln. 287 - ln. 316) decides on the ego car action based on the predition.
Based on the projection system determines if there a car ahead and if ego car should and can change lane. If it is impossible to change the lane then the ego car slows down to avoid collision.

### Trajectory
This part of the code (ln. 319 - ln. 421) performs trajectory calculation.
To calculate it system uses output of the Action part of the code together with car coordinates and past path points.
In the first part of the code, to initialise spline, the last two points of the previous trajectory (or the car position if previous trajectory is not present) together with three points in a distance are used.
Those points are used for spline calculation and the coordinates are transformed to the car's local coordinates.
The previous trajectory points are copied to the new trajectory in order to ensure its continuity. Remaining points are calculated based on the spline.
The speed chagne is decided on the Action result and it is applied on complete trajectory in order to increase "smoothness" of speepd chaneges. I tried applying speed chagne on every trajectory points but that resulted in less "smooth" driving experience.
_Possible improvement_ for this part of the code would be to better manage speed changes in case when we can't change the lane. The ego car should keep more "constant" speed based on the speed of the car that is ahead of it.
