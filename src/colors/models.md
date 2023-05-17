# Color Models

A color model is a method of representing colors in a video or image using data. This guide will be covering the most widely used color models.

## RGB

RGB is probably the most well-known color model, and is primarily used in image encoding. RGB consists of three color channels, Red, Green, and Blue, which are then combined to determine the final color of each pixel. Typically, RGB is the final colorspace that a monitor or TV will use to display images, although it is not commonly used for video encoding.

## YUV

YUV, also known as YCbCr, is the most widely used color model for video encoding. It consists of three planes: Y aka Luma, which represents luminance or brightness, and two chroma planes, which represent color. Generally a video player will have to convert a YUV video into RGB before it can be rendered, but there are significant compression benefits to using YUV over RGB for video.

The most notable reason is that a planar color model allows for an optimization called chroma subsampling. This means that the chroma planes can be encoded at a lower resolution than the luma plane, which results in a smaller output file.

### When to use chroma subsampling

There are three widely used variants of chroma subsampling:

- 4:2:0 which has half the vertical and horizontal chroma resolution
- 4:2:2 which has half the horizontal chroma resolution but full vertical resolution
- 4:4:4 which has full chroma resolution

4:2:2 is not particularly useful over the other options, so this guide will focus on 4:2:0 and 4:4:4.

4:2:0 is the most commonly used format for videos. Nearly every DVD, blu-ray, YouTube video, etc. uses 4:2:0 subsampling. This is because, in the majority of cases, human eyes do not notice the reduction in chroma resolution. There is very little benefit to using 4:4:4 in the average case.

However, there are some exceptions. The most notable is screen recordings. Things like text overlays, video game UI overlays, etc. have very fine, color-dependent detail that can be destroyed by chroma subsampling and result in an aliased look to the video. Therefore, it is recommended to use 4:4:4 subsampling when recording your desktop, and 4:2:0 subsampling in most other cases.
