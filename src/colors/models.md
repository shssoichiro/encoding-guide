<!-- TODO: expand on alpha -->
# Color Models

A color model is a method of
representing colors in a video or image using data. This guide will be
covering the most widely used color models.

## RGB

RGB is probably the most well-known color model, and is primarily used
in image encoding. RGB consists of three color channels, Red, Green,
and Blue, which are then combined to determine the final color of each
pixel. Typically, RGB is the final model that a monitor or TV
will use to display images, although it is not commonly used for video
encoding.

## YUV

YUV, also known as YCbCr, is the most widely used color model for
video encoding. It consists of three components: Y aka Luma, which
represents luminance or brightness, and two chroma planes, which
represent color. Generally a video player will have to convert a YUV
video into RGB before it can be rendered, but there are significant
compression benefits to using YUV over RGB for video.

The most notable reason to use YCbCr is an optimization called chroma
subsampling. This means that the chroma components can be encoded at a
lower resolution than the luma components, which results in a smaller
output file. You can read more about chroma subsampling in [Color
formats](./formats.md).
