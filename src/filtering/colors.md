# Bit Depths and Color Formats

A generic overview to colorimetry is presented in the [Color Management](./colors.md) section. This area will go more into detail on how colorimetry relates to video filtering, and how to modify colorimetry as part of your filter chain.

## Bit Depth

Historically, the majority of videos have been encoded using 8-bits of data per pixel. However, that is changing, especially with HDR becoming more and more popular. Modern encoders, including x265 and all AV1 encoders, support encoding at higher bit depths, and 10-bit encoding is becoming more common and recommended. (Note that although x264 also supports 10-bit encoding, some players may not support playback of 10-bit H.264, so if set-top compatibility is important, 10-bit H.264 should be avoided. It will however playback just fine on PC media players.)

In addition, when filtering, we typically want to run our filters on a 16-bit video to ensure the highest quality filtering possible.

We can account for these needs using functions from the [vstools](https://github.com/Irrational-Encoding-Wizardry/vs-tools) Vapoursynth plugin.

```python
import vstools

clip = core.lsmas.LWLibavSource(source="My Video.mkv")
clip = vstools.initialize_clip(clip)
# We can do other filtering here
clip = vstools.finalize_clip(clip)
```
