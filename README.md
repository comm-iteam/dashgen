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
                  [-fps FRAMES_PER_SECOND] [-psnr] [--clean]
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
  --clean               Remove segment files
```

Where codecs could be one of libx264, libx265 or vp9

A command example would be:
```
python3 dashgen.py -c vp9 -q 40 50 60 -ss 10 -fps 24 -psnr --clean tos.y4m
```

And the resulting psnr values will be found on the generated psnr_XXX.json where XXX could
be ```crf``` or ```bitrate```