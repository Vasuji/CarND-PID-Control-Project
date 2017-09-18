### Hyperparameter tuning.

The P, or "proportional", component had the most directly observable effect on the car's behavior.
It causes the car to steer proportional (and opposite) to the car's distance from the lane center 
(which is the CTE) - if the car is far to the right it steers hard to the left, if it's slightly 
to the left it steers slightly to the right.

The D, or "differential", component counteracts the P component's tendency to ring and overshoot the
center line. A properly tuned D parameter will cause the car to approach the center line smoothly without ringing.


The I, or "integral", component counteracts a bias in the CTE which prevents the P-D controller from 
reaching the center line. This bias can take several forms, such as a steering drift (as in the Control unit lessons), 
but I believe that in this particular implementation the I component particularly serves to reduce the CTE around curves.



1. Initially, I started with P, I, and D coefficients from the lessons (i.e. Kp = 0.2, Ki = 0.004, Kd = 3.0), but this
caused my car to turn very sharply, oscillating back and forth and then promptly run off the track.

2. I lowered all of the values until I had steering angles within the model tolerance of [-1, 1].  I still found that my
car was difficult to keep centered in the lane, so I also lowered the speed from 0.3 to 0.1

3. I found I was able to stay on the track with Kp = 0.10, Ki = 0.0000000006, Kd = 0.0019.  I found that the left turn after
bridge was much easier to navigate than the following right turn around the lake because the I term was compensating for
average left-hand turn due to the counter-clockwise lap.

4. I used manual tuning, running the simulator each time and comparing my results.

5. As I increased the P coefficient, I noticed that I needed a much larger corresponding increase in the D coeffecient,
otherwise the car would oscillate around the center of the track but never drive straight.

6. I finally settled on Kp = 0.18, Ki = 0.0000001, Kd = 0.2 as the hyperparemeters form my PID controller.  I found the
larger D value gave smoother driving and keeping the I term low reduced the left-hand bias.
