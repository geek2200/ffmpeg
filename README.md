# ffmpeg code
1. Code for watermarking logo on video in x=10 and y=10 between 0,2 secs
```
ffmpeg -i t0.mp4 -i logo.jpg -filter_complex "[0:v][1:v] overlay=10:10:enable='between(t,0,2)'" o.mp4
```
2. two watermark 
```
ffmpeg -i in.mp4 -i logo.mp4 -i name4.png -filter_complex "[0:v][1:v] overlay=0:0:enable='between(t,0,2.5)' [tmp]; [tmp][2:v] overlay=5:5:enable='between(t,3,50)'" o2.mp4
```

# procedure :
1. download video 
2. convert video to mp4 if needed 
```
ffmpeg -i input.webm input.mp4
```
3. extract frame from video 
```
ffmpeg -i input.mp4 -ss 00:01:55 -vframes 1 thumb.jpg
```
4. image convert to 1 sec video 
```
ffmpeg -loop 1 -i thumb.jpg -c:v libx264 -t 1 -pix_fmt yuv420p imagevideo.mp4
```
5. watermark

6. concat three videos 
```
ffmpeg -i imagevideo.mp4 -i videowatermarked.mp4 -i motion.mp4 -filter_complex "[0:v:0][0:a:0][1:v:0][1:a:0][2:v:0][2:a:0]concat=n=3:v=1:a=1[outv][outa]" -map "[outv]" -map "[outa]" output.mp4
```

# bodyvids :
1. read file from db and extract filename and muscle and name
2. based on muscle choose banner
3. overlay main banner on videos and output name is modify1 
```
ffmpeg -i test.mp4 -i first.mp4 -filter_complex "[0:v][1:v] overlay=0:0:enable='between(t,0,3)'" o.mp4
```
4. overlay lower banner on modify2 and name is modify2
```
ffmpeg -i o.mp4 -i banner.mov -filter_complex "[0:v][1:v]overlay=0:200:enable='between(t,0,13)'" o2.mp4
```
5. overlay top banner and modify3 
```
ffmpeg -i o2.mp4 -i top.mov -filter_complex "[0:v][1:v]overlay=0:0:enable='between(t,0,20)'" o3.mp4
```
6. and name text by ffmpeg in the lower right (find way for add perisan name)

# TV maker and add text as Wartermark

```
$file = __DIR__.'/test.mp4';
$dest = __DIR__.'/test1.mp4';
$option =[
    'targetFeed' => \InstagramAPI\Constants::FEED_STORY,
    //'blurredBorder'=>true,
    'operation'=> 2, // 1 is for crop, 2 is for expand
    'bgColor'=>[0,0,0]

];
$fontfile = __DIR__.'/../../../public/fonts/Gandom.ttf';
//$video = new \InstagramAPI\Media\Video\InstagramVideo($file,$option);
//copy($video->getFile(),$dest);
$s = '"drawtext=text_shaping=1:fontfile='.$fontfile.': \text=\'سلام\': fontcolor=white: fontsize=24: box=1: boxcolor=black@0.5: \
boxborderw=5: x=(w-text_w)/2: y=(h-text_h)/2"';
$d = "ffmpeg -i \"".$dest."\" -vf ".$s." -codec:a copy output.mp4";
echo $d;
//dd();
shell_exec($d);
```

# Draw text with fribidi
```
D:\ff\media-autobuild_suite-master\local64\bin-video\ffmpeg -i test.mp4 -vf drawtext="text_shaping=1:fontfile=E\/:/projectNew/assets/fonts/calibri.ttf':text='سلام':fontcolor=white:fontsize=36: box=1: boxcolor=red@0.5:boxborderw=5: x=(w-text_w)/2: y=100" -codec:a copy out.mp4
```
# Add audio to video 
```
ffmpeg -y -i test.mp4 -i s1.mp3 -c:v copy -map 0:v:0 -map 1:a:0 -c:a aac -b:a 192k -shortest new.mp4
```

