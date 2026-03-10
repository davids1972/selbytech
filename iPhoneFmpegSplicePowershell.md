#Powershel commant to spice 3 iphone videos together with audio and smooth transitions
ffmpeg `
-ss 00:04 -to 00:17 -i IMG_8425.MP4 `
-ss 00:29 -to 00:53 -i IMG_8425.MP4 `
-ss 00:20 -to 00:35 -i IMG_8427.MP4 `
-ss 00:05 -to 00:20 -i IMG_8428.MP4 `
-ss 02:04 -to 02:33 -i IMG_8428.MP4 `
-ss 01:04 -to 01:38 -i IMG_8428.MP4 `
-ss 03:42 -to 03:54 -i IMG_8428.MP4 `
-filter_complex "
color=c=black:s=720x1280:d=3,format=yuv420p,fps=30,settb=1/30,setpts=PTS-STARTPTS[titlebase];
[titlebase]drawtext=text='Quepos':
fontcolor=#4da6ff:
fontsize=78:
fontfile=C\\:/Windows/Fonts/arialbd.ttf:
x=(w-text_w)/2:
y=(h/2)-90:
shadowcolor=black:
shadowx=4:
shadowy=4[title1];
[title1]drawtext=text='Turtle Release':
fontcolor=#4da6ff:
fontsize=64:
fontfile=C\\:/Windows/Fonts/arialbd.ttf:
x=(w-text_w)/2:
y=(h/2)+10:
shadowcolor=black:
shadowx=4:
shadowy=4[titlev];
anullsrc=r=48000:cl=stereo:d=3[titlea];

[0:v]scale=720:1280:force_original_aspect_ratio=decrease,pad=720:1280:(ow-iw)/2:(oh-ih)/2,setsar=1,fps=30,settb=1/30,setpts=PTS-STARTPTS,format=yuv420p,fade=t=in:st=0:d=1[v0];
[1:v]scale=720:1280:force_original_aspect_ratio=decrease,pad=720:1280:(ow-iw)/2:(oh-ih)/2,setsar=1,fps=30,settb=1/30,setpts=PTS-STARTPTS,format=yuv420p[v1];
[2:v]scale=720:1280:force_original_aspect_ratio=decrease,pad=720:1280:(ow-iw)/2:(oh-ih)/2,setsar=1,fps=30,settb=1/30,setpts=PTS-STARTPTS,format=yuv420p[v2];
[3:v]scale=720:1280:force_original_aspect_ratio=decrease,pad=720:1280:(ow-iw)/2:(oh-ih)/2,setsar=1,fps=30,settb=1/30,setpts=PTS-STARTPTS,format=yuv420p[v3];
[4:v]scale=720:1280:force_original_aspect_ratio=decrease,pad=720:1280:(ow-iw)/2:(oh-ih)/2,setsar=1,fps=30,settb=1/30,setpts=PTS-STARTPTS,format=yuv420p[v4];
[5:v]scale=720:1280:force_original_aspect_ratio=decrease,pad=720:1280:(ow-iw)/2:(oh-ih)/2,setsar=1,fps=30,settb=1/30,setpts=PTS-STARTPTS,format=yuv420p[v5];
[6:v]scale=720:1280:force_original_aspect_ratio=decrease,pad=720:1280:(ow-iw)/2:(oh-ih)/2,setsar=1,fps=30,settb=1/30,setpts=PTS-STARTPTS,format=yuv420p[v6];

[0:a]aresample=48000,asetpts=PTS-STARTPTS,afade=t=in:st=0:d=1[a0];
[1:a]aresample=48000,asetpts=PTS-STARTPTS[a1];
[2:a]aresample=48000,asetpts=PTS-STARTPTS[a2];
[3:a]aresample=48000,asetpts=PTS-STARTPTS[a3];
[4:a]aresample=48000,asetpts=PTS-STARTPTS[a4];
[5:a]aresample=48000,asetpts=PTS-STARTPTS[a5];
[6:a]aresample=48000,asetpts=PTS-STARTPTS[a6];

[titlev][v0]xfade=transition=fade:duration=0.5:offset=2.5[v01];
[titlea][a0]acrossfade=d=0.5[a01];

[v01][v1]xfade=transition=fade:duration=0.5:offset=15.0[v02];
[a01][a1]acrossfade=d=0.5[a02];

[v02][v2]xfade=transition=fade:duration=0.5:offset=38.5[v03];
[a02][a2]acrossfade=d=0.5[a03];

[v03][v3]xfade=transition=fade:duration=0.5:offset=53.0[v04];
[a03][a3]acrossfade=d=0.5[a04];

[v04][v4]xfade=transition=fade:duration=0.5:offset=67.5[v05];
[a04][a4]acrossfade=d=0.5[a05];

[v05][v5]xfade=transition=fade:duration=0.5:offset=96.0[v06];
[a05][a5]acrossfade=d=0.5[a06];

[v06][v6]xfade=transition=fade:duration=0.5:offset=129.5[outv];
[a06][a6]acrossfade=d=0.5[outa]
" `
-map "[outv]" -map "[outa]" `
-c:v libx264 -pix_fmt yuv420p -r 30 -profile:v high -level 4.1 `
-c:a aac -b:a 192k `
-movflags +faststart -preset fast -crf 20 `
quepos_turtle_release_final_xfades.mp4