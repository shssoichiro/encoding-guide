# Source Filters

Source filters are the way to import a video into a Vapoursynth script.

This article will be expanded in the future, but for now we will cover the most common source filter, which handles the vast majority of use cases.

## LSmashSource

[LSmashSource](https://github.com/AkarinVS/L-SMASH-Works) is a source filter which supports the vast majority of video formats and is capable of frame-accurate decoding and seeking.

We will see an example of using LSmashSource below:

```python
clip = core.lsmas.LWLibavSource(source="My Video.mkv")

clip.set_output(0)
```

This will load the video located at this filepath into the Vapoursynth script, and make it available in the `clip` variable for later use. The `set_output` call at the end tells Vapoursynth to export this clip to the program that is calling the script, e.g. vspipe or vapoursynth-preview.

Note that some video formats, such as VC1, may encounter issues when attempting to seek through them. For these formats, it is recommended to only encode them linearly, i.e. without seeking. This means when using tools such as av1an, it is recommended to transcode to a lossless intermediate first.
