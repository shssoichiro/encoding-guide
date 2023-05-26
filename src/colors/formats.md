<!-- TODO: explain chroma siting -->
# Color Formats
To represent color values, a format is agreed upon. Color formats are
made up of three things, the [order of the
components](#component-order), the [bit depth](#bit-depth), and
whether it is a [packed or a planar format](#packed-vs-planar). In
some cases, [endianness](#endianness) may be important.

## Component order
The order in which the components (which come from a [color
model](/colors/models.md)) are arranged is simply represented by
writing them out. For example, `RGB` for red first, then green, then
blue, or `BGR` for blue, green, red.

## Bit depth
A bit depth is how many bits are available to store the sample
value. There are two main ways to specify the bit depth in a :
- bits per component. Here, `RGB888` reads as `RGB color model, with 8
  bits for the red component, 8 bits for the green component, and 8
  bits for the blue component` and `RGB565` reads as `RGB color model,
  with 5 bits for the red component, 6 bits for the green component,
  and 5 bits for the blue component`.
- bits per sample. Here, `RGB24` reads as `RGB color model, with 24
  bits in total for the red, green, and blue components`. This is
  ambiguous, because one does not know exactly how many bits are
  allocated to each component. `RGB565`, `RGB556`, and `RGB655` (even
  though the latter ones do not make much sense as the eye is most
  sensitive to green light) all become `RGB16`.

## Packed vs planar
Components can be stored either packed, where all
components are interleaved (here, `RGB`):
```
Sample number:   1   2   3   4   5
Data:          RGB RGB RGB RGB RGB
```
or stored separately for each component:
```
Sample number: 1 2 3 4 5
Data:          R R R R R...
Data:          G G G G G...
Data:          B B B B B...
```

In planar formats, many operations can be easier to implement, as it
is possible to implement the algorithm once and then operate on all
planes. On the other hand, packed formats are simpler and often used
in hardware.[^vlc-wiki-yuv]


## Endianness
Different computer architectures store numbers differently. For more
information, visit [the Wikipedia article on
endianness](//wikipedia.org/wiki/Endianness). There are two main ways
to store numbers with more than 8 bits (1 is the least significant
byte and 4 is the most significant byte, here 4 bytes):
- Most significant byte first, little endian, `4321`. This is what
  x86-family processors use.
- Least significant byte first, big endian, `1234`. This is what
  PowerPC-family processors use.

This can be important for color formats, as some computers might store
it in their native endianness. VapourSynth doesn't seem to care about
endianness, but FFmpeg does.

For example, `RGB565` might store its two bytes in `12` or `21` order,
and if they are read in the wrong order, it will produce garbage.

## Chroma subsampling
In [Y'CbCr](./models.md#yuv) signals, there are three widely used
variants of chroma subsampling:

- 4:2:0 which has half the vertical and horizontal chroma resolution
- 4:2:2 which has half the horizontal chroma resolution but full
  vertical resolution
- 4:4:4 which has full chroma resolution (no subsampling)

4:2:2 is not particularly useful over the other options, so this guide
will focus on 4:2:0 and 4:4:4.

4:2:0 is the most commonly used format for videos. Nearly every DVD,
blu-ray, YouTube video, etc. uses 4:2:0 subsampling. This is because,
in the majority of cases, human eyes do not notice the reduction in
chroma resolution. There is very little benefit to using 4:4:4 in the
average case.

However, there are some exceptions. The most notable is screen
recordings. Things like text overlays, video game UI overlays,
etc. have very fine, color-dependent detail that can be destroyed by
chroma subsampling and result in an aliased look to the
video. Therefore, it is recommended to use 4:4:4 subsampling when
recording your desktop, and 4:2:0 subsampling in most other cases.

## Common formats
| [VS](/filtering/intro.md) name | [FFmpeg](/filtering/intro_ffmpeg.md) name                                   | Meaning                                                                                               |
|--------------------------------|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| `GRAY8`                        | `gray8`                                                                     | Brightness only, 8 bits, packed                                                                       |
| `GRAY16`                       | `gray16le`, `gray16be` (the suffix specifies the [endianness](#endianness)) | Brightness only, 16 bits                                                                              |
| `RGB888`                       | `rgb24`                                                                     | red, green, blue, 8 bits per component                                                                |
| `YUV420P8`                     | `yuv420p`                                                                   | luma, chroma blue, chroma red, 8 bits per component, planar, 4:2:0 [subsampling](#chroma-subsampling) |
| `YUV422P8`                     | `yuv422p`                                                                   | luma, chroma blue, chroma red, 8 bits per component, planar, 4:2:2 subsampling                        |
| `YUV444P8`                     | `yuv444p`                                                                   | luma, chroma blue, chroma red, 8 bits per component, planar, no subsampling                           |
| `YUV420P10`                    | `yuv420p10le`, `yuv420p10le`                                                | luma, chroma blue, chroma red, 10 bits per component, planar, 4:2:0 subsampling                       |
| `YUV422P10`                    | `yuv422p10le`, `yuv422p10le`                                                | luma, chroma blue, chroma red, 10 bits per component, planar, 4:2:2 subsampling                       |
| `YUV444P10`                    | `yuv444p10le`, `yuv444p10le`                                                | luma, chroma blue, chroma red, 10 bits per component, planar, no subsampling                       |

## References
[^vlc-wiki-yuv]: [YUV - VideoLAN Wiki](https://wiki.videolan.org/YUV/#Packed_formats)
