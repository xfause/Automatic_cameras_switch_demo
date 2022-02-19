# Camera automatic switching system based on optical flow and bone position

## Effect

![](https://s4.ax1x.com/2022/02/19/HbhGxs.gif)

## Principle

This system is suitable for automatic switching of camera splits in dance videos. It is based on the calculation of optical flow and bone position, and uses Beat as a node (hereinafter referred to as "shot").

Calculate the optical flow at the end of each shot and the end of the previous shot, which is used to represent the intensity of the action and other probabilistic models that do not understand dimensions.

Among multiple cameras with preset relative positions, the one with the highest calculated probability is selected as the current camera.

## Model calculation rules

- Guarantee the continuity of look and feel within a certain time range
  - In order to maintain the continuity in a certain shot, if the number of continuous shots in the current shot is less than a certain threshold, the probability that the next shot is still in this shot is 1, otherwise if it exceeds a certain threshold, the probability is -1, In addition, the probability that the next shot will be in a certain shot is uniformly distributed.
  - Guaranteed that the effect of frequent camera switching will not occur
- More leaning and switching between shots of different compositions
  - By calculating the average optical flow from the beginning of the motion to the current shot, switch based on the probability model in the camera with a larger average optical flow and a smaller average optical flow, so as to ensure that the composition is different.
- Increases the probability of being selected for cameras that are far away from the subject
  - Reflect the dance action content through the panorama
  - The closer the camera is, the shorter the duration in that shot, and vice versa.
- Set up a main camera
  - Increase the duration on the main camera to avoid lack of subject.
  - Use the bone position to take the proportion of the character model in the video screen as the main parameter
- Emphasize the rhythm, switch to a camera where the action is relatively farther away
  - Calculate the average optical flow and the optical flow of the previous shot. If the difference is large, the rhythm and movement are more intense.

The probability model obtained by combining the above five rules will give a series of probability values of whether to switch to this place, decide which camera should be switched to in the current shooting, and give corresponding switching special effects.

## Problems

- Efficiency issues for calculating optical flow
   - The official plug-in for opencv for unity is provided, but due to cost reasons, the free plug-in opencv plus unity is used, and there may be problems in the efficiency of calculating optical flow.
   - Since the calculated optical flow has a greater relationship with the resolution, the freeze is more serious when the resolution is higher.
- Probabilistic models are not perfect
   - There may be other more principles to follow in dance videos
- Automatic switching effects
   - Supports automatic switching of special effects, but the rules for choosing which special effects are relatively simple
   - Currently only supports gradient, hard cut, motion switching.
- Camera scaling issue
   - It is difficult to calculate the fov. Although the problem of different optical flow sizes caused by the different proportions of characters occupying the screen under different fovs is minimized by normalization, there are still errors.

## Notice

Because the free plugin I used in this project warned by author "Can't upload to github".

So I package the code base in cloud, you can download here

link：https://pan.baidu.com/s/12iJGlMY30gpdPRjDeXR4kg

password：7hfw
