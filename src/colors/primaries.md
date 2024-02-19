# Color Primaries

This section enters the first of three settings that are important for retaining accurate color when encoding videos, those settings being primaries, color matrix, and transfer characteristics.

Color primaries are used to indicate the correct coordinates for the red, blue, and green colors. There are historical reasons for [why so many standards exist](https://xkcd.com/927/), and this guide will not go in depth into history lessons, but will explain what primaries are available and when to use each one.

Note that for primaries, matrices, and transfer, you can view the values that are set on a video using a tool like [MediaInfo](https://mediaarea.net/en/MediaInfo). If there are no values set, the renderer will need to guess which values to use. A safe default assumption for most modern videos is BT.709, although this may vary depending on source and resolution for the video. It is strongly preferred to set the correct values when encoding.

Each setting has at least one name and exactly one integer value representing it--most encoder softwares will accept one or more of the names, but some tooling such as Vapoursynth and MKVToolnix accepts the integer values instead.

In case no color primaries are specified, `mpv` uses the following heuristics:

```
if matrix == "BT.2020" {
    "BT.2020"
} else if matrix == "BT.709" {
    "BT.709"
} else if width >= 1280 || height > 576 {
    "BT.709"
} else if height == 576 {
    "BT.470BG"
} else if height == 480 || height == 488 {
    "SMPTE 170M"
} else {
    "BT.709"
}
```

### BT.709

BT.709 is the standard used for modern high-definition video, and is a safe default assumption.

These color primaries are used in the following standards:

- Rec. [ITU-R BT.709](https://www.itu.int/rec/R-REC-BT.709/en)-6
- Rec. ITU-R BT.1361-0 conventional colour gamut
  system and extended colour gamut system (historical)
- IEC 61966-2-1 sRGB or sYCC
- IEC 61966-2-4
- Society of Motion Picture and Television Engineers
  (SMPTE) RP 177 (1993) Annex B

The color primaries specified by BT.709 are ([1](https://en.wikipedia.org/w/index.php?title=Standard_illuminant&oldid=1207711650), [2](https://en.wikipedia.org/w/index.php?title=Rec._709&oldid=1193725571)):

|   | R    | G   | B    | White point (D65) |
|---|------|-----|------|-------------------|
| x | 0.64 | 0.3 | 0.15 | 0.31272           |
| y | 0.33 | 0.6 | 0.06 | 0.32903           |

### SMPTE 170M

SMPTE 170M is a stanrard that was used for NTSC television systems and DVDs.

- Rec. [ITU-R BT.601](https://www.itu.int/rec/R-REC-BT.601/en)-7 525
- Rec. ITU-R BT.1358-1 525 or 625 (historical)
- Rec. ITU-R BT.1700-0 NTSC
- SMPTE ST 170 (2004)
- SMPTE 240M, an interim standard used during the early days of HDTV (1988-1998).

### BT.470BG

BT.470BG is a standard that was used for European (PAL) television systems and DVDs.

These color primaries are used in the following standards:

- Rec. [ITU-R BT.470](https://www.itu.int/rec/R-REC-BT.470/en)-6 System B, G (historical)
- Rec. [ITU-R BT.601](https://www.itu.int/rec/R-REC-BT.601/en)-7 625
- Rec. ITU-R BT.1358-0 625 (historical)
- Rec. ITU-R BT.1700-0 625 PAL and 625 SECAM

The color primaries specified by BT.601 for 625-line video are ([1](https://en.wikipedia.org/w/index.php?title=Standard_illuminant&oldid=1207711650), [2](https://www.itu.int/dms_pubrec/itu-r/rec/bt/R-REC-BT.601-7-201103-I!!PDF-E.pdf):
|   | R    | G    | B    | White point (D65) |
| x | 0.64 | 0.29 | 0.15 | 0.31272           |
| y | 0.33 | 0.6  | 0.06 | 0.32903           |


### BT.470M

BT.470M is a standard that was used in analog television systems in the United States.

These color primaries are used in the following standards:

- Rec. [ITU-R BT.470](https://www.itu.int/rec/R-REC-BT.470/en)-6 System M (historical)
- United States National Television System Committee
  1953 Recommendation for transmission standards for
  color television
- United States Federal Communications Commission
  (2003) Title 47 Code of Federal Regulations 73.682 (a) (20)

### Film

The White point used by color film is Standard Illuminant C (??? I'm not sure if this makes any sense whatsoever).

### BT.2020

BT.2020 is a standard used for ultra-high-definition video, i.e. 4K and higher. It may be used with or without HDR, as HDR is defined by the transfer characteristics.

These color primaries are used in the following standards:

- Rec. [ITU-R BT.2020](https://www.itu.int/rec/R-REC-BT.2020-2-201510-I/en)-2
- Rec. ITU-R BT.2100-2

The color primaries specified by BT.2020 are ([1](https://en.wikipedia.org/w/index.php?title=Standard_illuminant&oldid=1207711650), [2](https://www.itu.int/dms_pubrec/itu-r/rec/bt/R-REC-BT.2020-2-201510-I!!PDF-E.pdf):

|   | R     | G     | B     | White point (D65) |
|---|-------|-------|-------|-------------------|
| x | 0.708 | 0.170 | 0.131 | 0.31272           |
| y | 0.292 | 0.797 | 0.046 | 0.32903           |

### SMPTE 428

SMPTE 428 is used for D-Cinema Distribution Masters, aka DCDM.

These color primaries are used in the following standards:

- SMPTE ST 428-1 (2019)
- (CIE 1931 XYZ as in ISO 11664-1)

### DCI-P3

DCI-P3 is a wide-gamut colorspace used alongside RGB. It is used internally by most HDR monitors on the market.

### Display-P3

Display-P3 is a variant of DCI-P3 developed by Apple because they wanted to be different.

### EBU Tech 3213

EBU Tech 3213 is a standard for studio monitors, apparently. It is used in the following standard:

- [EBU Tech 3213](https://tech.ebu.ch/docs/tech/tech3213.pdf) (duh)

The color primaries specified by EBU Tech 3213 are the same as BT.470BG. It uses the D65 white point
as well.
