# Video Formats

Before we can begin encoding, we have to have a basic understanding of what encoding _is_.
Encoding is essentially compressing the video or audio so that it results in a smaller file.
This is similar to what you might have done with .rar or .zip files, the difference being
that video and audio encoders are highly specialized, allowing for far greater compression
than a generic format could give.

There have been hundreds of video compression formats across the decades, but as technology has advanced,
allowing the creation of better and better formats, this guide will only cover the most popular formats that are still worthwhile for encoding today.

## Lossy Encoding

"Lossy" encoding refers to a type of video compression where there is information lost between the source and the encode. This may include artifacts such as banding, blocking, ringing, blurring, etc., and generally the smaller the output file is, the more artifacts it tends to have. This is the predominant type of compression used in video encoding, as it results in much smaller files, and the quality loss is generally considered acceptable. Modern encoders attempt to reduce the amount of artifacts that are created at an equivalent bitrates, so that they can produce smaller files that look better.

### H.264

H.264 has been around for almost 20 years now, and has remained the most popular video format throughout most of this period. Until recently with the rise in popularity of HDR, it has been the primary format used by streaming services and on Blu-ray discs, as well as by many digital video cameras, and is still extremely common today. It is also extremely popular among hobbyist encoders due to the presence of x264, which is a highly advanced, fast, free and open-source encoder for the H.264 format.

### H.265

H.265 is the successor to the H.264 format, and includes more advanced features for compression as well as support for HDR, or High Dynamic Range, which is a technology that allows increased contrast (and by extension visual appeal) of a video. H.265 also has a popular, advanced, and free open-source encoder, called x265, which has become more developed over the years and now is every bit as advanced as x264. H.265, for now, is the recommended format for use with any HDR videos. However, one major limitation of H.265 is that most browsers will not playback H.265 natively, making it difficult to use for internet streaming, although some providers such as Netflix have adapted their services to support H.265.

### VP9

VP9 is a video format developed by Google, and is predominantly used by YouTube. It achieves similar compression to H.264, and is free of patent restrictions. It also has a free, open-source encoder, called vpxenc, although this encoder has not developed to the point of x264. As a result, vpxenc is still quite slow and does not necessarily achieve the full quality that the VP9 format is capable of.

### AV1

AV1 is the successor to VP9, and is the joint work of many major companies. Like VP9, it intends to be patent-free, but it brings many compression improvements not just from its own design, but from other codecs which were in development at the time, such as Daala and Thor. AV1 currently has three major open-source encoders: aomenc, which is the reference encoder developed predominantly by Google; SVT-AV1, which is focused heavily on speed and multithreading; and rav1e, which was originally sponsored by Mozilla, and aims to be more focused on psychovisual features (i.e. more appealing to human eyes) than the other two encoders. AV1 playback is currently supported in all major browsers and by most phones and tablets, and is beginning to be supported by newer set-top devices such as the Fire Stick 4k Max. Although there is still plenty of work to be done for any AV1 encoder to reach its full potential, AV1 appears to be the future of video encoding.

## Lossless Encoding

Unlike lossy encoding, lossless encoding is a type of encoding where the output is exactly identical to the input. The reason why one might do this is to apply filtering such as resizing, debanding, tonemapping, etc. to a video prior to lossy encoding. This could be encoded directly to lossy in one step, but sometimes the addition of a lossless encoding step makes more sense either from a workflow standpoint or from an encoding performance standpoint.

### H.264

x264 is capable of encoding videos losslessly, and it is quite good at it. Generally, this is going to be one of the best options for lossless video encoding, as it is fast, compresses well, and has support for 10-bit encoding. Given that using a slower preset does not increase quality, but only reduces filesize, and that lossless files are often used only as intermediates or temporary files, it is common to use an x264 preset such as veryfast for lossless.

### FFv1

FFv1 is a lossless codec included with the encoding tool ffmpeg. It is solely intended for lossless encoding, and can losslessly store up to 16-bit video. However, it does not compress as well as H.264 and tends to be slower at both encoding and decoding, particularly if using a fast x264 preset.
