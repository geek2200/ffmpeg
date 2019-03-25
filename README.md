# ffmpeg code
1. Code for watermarking logo on video in x=10 and y=10 between 0,2 secs
```
ffmpeg -i t0.mp4 -i logo.jpg -filter_complex "[0:v][1:v] overlay=10:10:enable='between(t,0,2)'" o.mp4
```
