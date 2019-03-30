# ffmpeg code
1. Code for watermarking logo on video in x=10 and y=10 between 0,2 secs
```
ffmpeg -i t0.mp4 -i logo.jpg -filter_complex "[0:v][1:v] overlay=10:10:enable='between(t,0,2)'" o.mp4
```
2. two watermark 
```
ffmpeg -i in.mp4 -i logo.mp4 -i name4.png -filter_complex "[0:v][1:v] overlay=0:0:enable='between(t,0,2.5)' [tmp]; [tmp][2:v] overlay=5:5:enable='between(t,3,50)'" o2.mp4
```
