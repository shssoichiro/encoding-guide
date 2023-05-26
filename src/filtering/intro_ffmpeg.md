# Introduction to the FFmpeg command-line utilities
[FFmpeg](//ffmpeg.org) is a multimedia framework that has utilities
for transcoding, transmuxing, and filtering audio and video. It
provides the [`ffmpeg`](#using-the-ffmpeg-program), ffprobe, and
ffplay command-line utilities. It also features the libav\* libraries,
which allow you to use the functionality of FFmpeg without the
programs.[^multimediawiki-howtos]

## Obtaining FFmpeg
### Unix-like
#### Package manager
The easiest way to obtain FFmpeg is through your package manager. On
most package managers, the package is simply named `ffmpeg`, however,
`ffprobe` and `ffplay` may have their own packages. Note that the
packages may be outdated.

#### Compiling from source
To compile FFmpeg from source:
- grab [the sources](//ffmpeg.org/download.html).
- Run `./configure --help` to see a list of features and libraries you
  can choose to build with.
- Install all libraries you want to build FFmpeg with
- Run `./configure` with all `--enable-` flags you want.
- Run `make`.
- Run `make install`.

#### Binary packages
These packages are not compiled by FFmpeg themselves. Be careful.

- [John van Sickle](//johnvansickle.com/ffmpeg/)

### Windows
<!-- TODO: I have no clue how the windows users compile. I recommend MinGW. -->

#### Binary Packages
These packages are not compiled by FFmpeg themselves. Be careful.

- [gyan.dev](//gyan.dev/ffmpeg/builds/)

## Using the `ffmpeg` program
`ffmpeg` is the primary command-line tool of `FFmpeg`. It takes 0 or
more [bitstreams](#bitstream) as inputs and outputs.

### Concepts
#### Bitstream
A *bitstream* or *bit stream* is a media file, the kind that is played
in a media player. It consists of a [container](#container) wrapping multiple
[elementary streams](#elementary-stream)

#### Container
A container is a format for putting one or more [elementary
streams](#elementary-stream) intro one file, or
[bitstream](#bitstream).

#### Elementary stream
An elementary stream is an audio, video, or subtitle track. Basically,
it's the compressed data you want to [mux](#muxing) into the container.

#### Muxing
Putting elementary streams into a container.

#### Codec
A codec (**co**der/**dec**oder) is the piece of code that actually
encodes the data you put in. It takes as input and produces as output
an elementary stream.

#### Filter
A filter is a piece of code you can apply to the data to
make something about it different, for instance sharpening,
removing artifacts, shakiness, denoising, scaling, overlay, etc.

#### Muxer/Demuxer
The pieces of code that [mux](#muxing) or do the reverse, getting
elementary streams from the container.

#### Bitstream filter
A bitstream filter is a filter that is directly applied to the
[bitstream](#bitstream) in order to change something about the
container, for instance, convert frame types, or corrupt some packets.

### Command-line arguments

`ffmpeg`s command-line arguments are positional. That means, it
matters where you put options. Each input and output has their own
arguments. So, for example `ffmpeg -r 24 -i file1 file2` applies the
`-r 24` option to the input `file1`, interpreting the video as having
that frame rate, while `ffmpeg -i file1 -r 24 file2` applies the `-r
24` option to `file2`. To get a list of options, refer to the [FFmpeg
documentation](//ffmpeg.org/ffmpeg-all.html).

### How do I...

#### Transcode a video
`ffmpeg -i input -c:v video_codec -b:v video_bitrate -c:a
audio_codec -b:a audio_bitrate output`

| Option               | Meaning                                                     |
|----------------------|-------------------------------------------------------------|
| `-c:v video_codec`   | **c**odec for the automatically selected **v**ideo stream   |
| `-b:v video_bitrate` | **b**itrate for the automatically selected **v**ideo stream |
| `-c:a audio_codec`   | **c**odec for the automatically selected **a**udio stream   |
| `-b:a audio_bitrate` | **b**itrate for the automatically selected **a**udio stream |

#### Transmux a video
`ffmpeg -i input -c copy output`

| Option    | Meaning                       |
|-----------|-------------------------------|
| `-c copy` | set the **c**odec to **copy** |

#### Filter a video
`ffmpeg -i input -c:v video_codec -c:a audio_codec (...) -vf filter_name output`

| Option            | Meaning                                         |
|-------------------|-------------------------------------------------|
| `-vf filter_name` | set the **v**ideo **f**ilter to **filter_name** |

## References
[^multimediawiki-howtos]: [HOWTO Search Results - MultimediaWiki](//wiki.multimedia.cx/index.php?search=HOWTO&title=Special%3ASearch&go=Go)
