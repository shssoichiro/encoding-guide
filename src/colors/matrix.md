# Matrix Coefficients

Matrix coefficients represent the multiplication matrix that is used when converting from YUV to RGB.

`mpv` will use the following heuristics when the color matrix is not known:

```
if width >= 1280 || height > 576 {
    "BT.709"
} else {
    "SMPTE 170M"
}
```

The following values are available:

### Identity

Specifies that the identity matrix should be used, i.e. this data is already in an RGB colorspace.

This matrix coefficient setting is used in the following standards:

- RGB
- XYZ
- IEC 61966-2-1 sRGB
- SMPTE ST 428-1 (2019)

This matrix is given by:

|   |   |   |
|---|---|---|
| 1 | 0 | 0 |
| 0 | 1 | 0 |
| 0 | 0 | 1 |

### BT.709

BT.709 is the standard used for modern high-definition video, and is a safe default assumption.

This matrix coefficient setting is used in the following standards:

- Rec. ITU-R BT.709-6
- Rec. ITU-R BT.1361-0 conventional colour gamut system and extended colour
  gamut system (historical)
- IEC 61966-2-4 xvYCC709
- SMPTE RP 177 (1993) Annex B

This matrix is given by ([1](https://en.wikipedia.org/w/index.php?title=YCbCr&oldid=1203379996)):
|   |         |         |
|---|---------|---------|
| 1 | 0       | 1.5748  |
| 1 | -0.1873 | -0.4861 |
| 1 | 1.8556  | 0       |

### BT.470M

BT.470M is a standard that was used in analog television systems in the United States.

### BT.470BG

BT.470BG is a standard that was used for European (PAL) television systems and DVDs.

This matrix coefficient setting is used in the following standards:

- Rec. ITU-R BT.470-6 System B, G (historical)
- Rec. ITU-R BT.601-7 625
- Rec. ITU-R BT.1358-0 625 (historical)
- Rec. ITU-R BT.1700-0 625 PAL and 625 SECAM
- IEC 61966-2-1 sYCC
- IEC 61966-2-4 xvYCC601

### SMPTE 170M

SMPTE 170M is a stanrard that was used for NTSC television systems and DVDs. Its matrix coefficients are equivalent to BT.470BG.

This matrix coefficient setting is used in the following standards:

- Rec. ITU-R BT.601-7 525
- Rec. ITU-R BT.1358-1 525 or 625 (historical)
- Rec. ITU-R BT.1700-0 NTSC
- SMPTE ST 170 (2004)

### SMPTE 240M

SMPTE 240M was an interim standard used during the early days of HDTV (1988-1998).

### YCgCo

The YCoCg color model, also known as the YCgCo color model,
is the color space formed from a simple transformation of
an associated RGB color space into a luma value and
two chroma values called chrominance green and chrominance orange.

### BT.2020 Non-Constant Luminance

BT.2020 is a standard used for ultra-high-definition video, i.e. 4K and higher. It may be used with or without HDR, as HDR is defined by the transfer characteristics. If you do not know if you want non-constant or constant luminance, you probably want non-constant.

This matrix coefficient setting is used in the following standards:

- Rec. ITU-R BT.2020-2 (non-constant luminance)
- Rec. ITU-R BT.2100-2 Y′CbCr

### BT.2020 Constant Luminance

This is a variant of BT.2020 with constant luminance values, represented using the YcCbcCrc colorspace. You probably want the non-constant luminance variant instead, unless you know you want this one.

### SMPTE 2085

SMPTE 2085 is a standard used with HDR signals in the XYZ colorspace. I've never actually seen it used in the wild.

### Chromaticity-Derived Non-Constant Luminance

I'm not really sure when you would use this.

### Chromaticity-Derived Constant Luminance

I'm not really sure when you would use this.

### ICtCp

ICtCp is an alternative colorspace developed for use with HDR and wide gamut video, by Dolby because they love doing extra stuff like this. I've never actually seen it used in the wild.
