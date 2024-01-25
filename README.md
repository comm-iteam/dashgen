# dashgen

Dashgen is a tool to create dash-prepared videos for testing purposes.
It feature list is:

* Encode video based on a bitrate list or a CRF list
* Create all selected representations in one command
* Computes a segment-by-segment PSNR for the created representations

Show the help with ```python3 dashgen.py -h``` to show:
```
usage: dashgen.py [-h] [-q QUALITIES [QUALITIES ...] | -b BITRATES
                  [BITRATES ...]] -c CODEC -ss SEGMENT_SIZE
                  [-fps FRAMES_PER_SECOND] [-psnr] [-vmaf] [--clean]
                  video

Generate DASH Video

positional arguments:
  video

optional arguments:
  -h, --help            show this help message and exit
  -q QUALITIES [QUALITIES ...], --qualities QUALITIES [QUALITIES ...]
                        Encoding qualities(crf)
  -b BITRATES [BITRATES ...], --bitrates BITRATES [BITRATES ...]
                        Encoding bitrates(as ffmpeg likes: 500kbps, 1M...)
  -c CODEC, --codec CODEC
                        Coded (ffmpeg)
  -ss SEGMENT_SIZE, --segment-size SEGMENT_SIZE
                        Segment size(s)
  -fps FRAMES_PER_SECOND, --frames-per-second FRAMES_PER_SECOND
                        Frames per second
  -psnr, --calculate-psnr
                        Calculate PSNR
  -vmaf, --calculate-vmaf
                        Calculate VMAF
  --clean               Remove segment files
```

Where codecs could be one of libx264, libx265 or vp9

A command example would be:
```
python3 dashgen.py -c vp9 -q 40 50 60 -ss 10 -fps 24 -psnr --clean tos.y4m
```

And the resulting psnr values will be found on the generated psnr_XXX.json where XXX could
be ```crf``` or ```bitrate```

Please considere reference this work if this software if useful for you:
```BibTeX
@article{DEFEZ2020126,
title = {New objective QoE models for evaluating ABR algorithms in DASH},
journal = {Computer Communications},
volume = {158},
pages = {126-140},
year = {2020},
issn = {0140-3664},
doi = {https://doi.org/10.1016/j.comcom.2020.05.011},
url = {https://www.sciencedirect.com/science/article/pii/S0140366419312800},
author = {Ismael {de Fez} and Román Belda and Juan Carlos Guerri},
keywords = {Quality of Experience (QoE), Dynamic Adaptive Streaming over HTTP (DASH), Peak Signal-to-Noise Ratio (PSNR), Video Multimethod Assessment Fusion (VMAF), Adaptive Bitrate Streaming (ABR), ITU-T P.1203},
abstract = {As users become more demanding with regards to the consumption of multimedia content, the importance of measuring their level of satisfaction is growing. The difficulty in terms of time and resources for assessing the Quality of Experience (QoE) has popularized the use of objective QoE models, which try to emulate human behavior regarding the playback of multimedia streaming. Some objective QoE models existing in the literature are based on the bitrate. However, the PSNR (Peak Signal-to-Noise Ratio) or VMAF (Video Multimethod Assessment Fusion) have been proved to be metrics with a closer relationship with the QoE than the bitrate. This paper proposes three new models to measure the QoE analytically in DASH (Dynamic Adaptive Streaming over HTTP) video services. The first is based on the bitrate of the displayed video segments, whereas the second and the third are based on the PSNR and VMAF of each video segment, respectively. The proposed models are compared to the ITU-T standard P.1203 as well as the bitrate-based QoE model proposed by Yin et al. Moreover, the paper presents a subjective study, which confirms the validity of the proposed models. The models are validated by using different DASH adaptation algorithms. In this sense, this paper also presents a DASH ABR (Adaptive Bitrate Streaming) algorithm called Look Ahead, which takes into account the inherent bitrate variability of the video encoding process in order to calculate, in real time, the appropriate quality level that minimizes the number of stalls during the playback.}
}
```
