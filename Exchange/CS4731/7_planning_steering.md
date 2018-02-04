# (Kinematic) Movement, Steering, Flocking, Formations
General Idea: character has some state information such as position and velocity.

Mod 2pi: guarantees that it goes over 2PI, you end up wrapping back.

## Statics
Static because there are no information about the movement.

What do movement algorithms output?
- Where do i end up (location)
- Where do i face (facing, not always necessary)

Moving characters are described by:
- Position
- Orientation
- Velocity
- Rotation

In general movement behaviours will output a velocity and rotation which follows the behaviours of the character.

## Time and Variable Frame Rates
Frame rate is often variable, even in a single device, we can't count on it.

## Kinematic Updates to Position & Orientation
Is often really tiny on game engines. So we usually cross out parts of the algorithm.

## Facing
Can be done by tying to the movement, or to do it independently:
- Can be done by doing turning after movement is finished, looks weird unless this is what we are trying to achieve
- Can be done by smoothing if we know how long the movement is going to take.

## Seek, Arrive, Flee, and Wander
Seek and Flee both directs toward to a target position. Seek will make the agent approach a target position, and for Flee we just need to negate that seek.

Arrival: seeking with full velocity will cause overshooting, so to do arrival, you do deceleration. You set an arrival circle, and once you've hit the arrival radius, you start decreasing your speed.

Wander: move in current direction, vary orientation by some amount each frame. This will create a wandering behaviour.

## Other Behaviours
- Following or chasing
- Pursuit / evade
- Hide
- Obstacle & wall avoidance
