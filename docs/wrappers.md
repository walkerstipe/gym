Gym includes numerous wrappers for environments that include preprocessing and various other functions. The following categories are included:

## Observation Wrappers

`DelayObservation(env, delay)` [text]
* Bring over from SuperSuit

`FilterObservation(env, filter_keys)` [text]
* Needs review (including for good assertion messages and test coverage)

`FlattenObservation(env)` [text]
* Needs good asseration messages

`FrameStack(env, num_stack, lz4_compress=False)` [text]
* Needs review (including for good assertion messages and test coverage)

`GrayScaleObservation(env)` [text] 
* Needs R/G/B channel argument added like supersuit wrapper
* Needs review (including for good assertion messages and test coverage)
* Needs CV2 dependency replaced with SuperSuit's way of doing full grey scaling: https://github.com/PettingZoo-Team/SuperSuit/blob/master/supersuit/utils/basic_transforms/color_reduction.py

`PixelObservationWrapper(pixels_only=True, render_kwargs=None, pixel_keys=("pixels",))` [text]
* Needs review (including for good assertion messages and test coverage)

`RescaleObservation(env, min_obs, max_obs`) [text]
* Bring over from Supersuit or from https://github.com/openai/gym/pull/1635

`ResizeObservation(env, shape)` [text]
* Needs review (including for good assertion messages and test coverage)
* Switch from CV2 to Lycon2 once released

`TimeAwareObservation(env)` [text]
* Needs review (including for good assertion messages and test coverage)

## Action Wrappers

`ClipAction(env)` [text]
* Needs review (including for good assertion messages and test coverage)

`ChangeDtype(env, dtype)` [text]
* Bring over from SuperSuit

`RescaleAction(env, min_action, max_action)` [text]
* Needs review (including for good assertion messages and test coverage)

`StickyActions(env, repeat_action_probability)` [text]
* Create as separate wrapper from Atari/bring over from SuperSuit

## Reward Wrappers

`ClipReward(env, lower_bound-1, upper_bound=1)` [text]
* Bring over from SuperSuit

## Lambda Wrappers

`ActionLambda(env, change_action_fn, change_space_fn)` [text]
* Bring over from SuperSuit

`ObservationLambda(env, observation_fn, observation_space_fn)` [text]
* Bring over from SuperSuit, replaces TransformObservation

`RewardLambda(env, reward_fn)` [text]
* Bring over from SuperSuit, replaces TransformReward

## Other
`AtariPreprocessing(env, noop_max=30, frame_skip=4, screen_size=84, terminal_on_life_loss=False, grayscale_obs=True, grayscale_newaxis=False, scale_obs=False)` [text]
* Needs review (including for good assertion messages and test coverage)

`RecordEpisodeStatistic(env)` [text]
* Needs review (including for good assertion messages and test coverage)

`RecordVideo(env, video_folder, record_video_trigger, video_length=0, name_prefix="rl-video")` [text]

The `RecordVideo` is a lightweight `gym.Wrapper` that helps recording videos. See the following
code as an example.

```python
import gym
env = gym.make("CartPole-v1")
env = gym.wrappers.RecordVideo(env, "videos", record_video_trigger=lambda x: x % 100 == 0)
observation = env.reset()
for _ in range(1000):
  env.render()
  action = env.action_space.sample() # your agent here (this takes random actions)
  observation, reward, done, info = env.step(action)

  if done:
    observation = env.reset()
env.close()
```

To use it, you need to specify the `video_folder` as the storing location and 
`record_video_trigger` as a frequency at which you want to record.

There are two modes of video the recording:
1. Episodic mode. 
    * By default `video_length=0` means the wrapper will record *episodic* videos: it will keep
    record the frames until the env returns `done=True`.
2. Fixed-interval mode.
    * By tuning `video_length` such as `video_length=100`, the wrapper will record exactly 100 frames
    for every videos the wrapper creates. 

Lastly the `name_prefix` allows you to customize the name of the videos.


`TimeLimit(env, max_episode_steps)` [text]
* Needs review (including for good assertion messages and test coverage)

Some sort of vector environment conversion wrapper needs to be added here, this will be figured out after the API is changed.
