# ffmpeg-hw-win32
ffmpeg 3.3.4  
gcc 7.2.0  
--enable-nvenc              
--enable-libmfx             
--enable-libfdk-aac         0.1.4  
--enable-libspeex           1.2  
--enable-libx264            git:r2721.72d53ab  
--enable-libx265            2.5  
--enable-libmp3lame         3.99.5  
--enable-libvpx             1.6.1  
--enable-libnpp

## Hardware acceleration methods:
```
dxva2
qsv
cuvid
```

## HW decoders:
```
 V..... h264_cuvid            (codec h264)
 V..... hevc_cuvid            (codec hevc)
 V..... mjpeg_cuvid           (codec mjpeg)
 V..... mpeg1_cuvid           (codec mpeg1video)
 V..... mpeg2_cuvid           (codec mpeg2video)
 V..... mpeg4_cuvid           (codec mpeg4)
 V..... vc1_cuvid             (codec vc1)
 V..... vp8_cuvid             (codec vp8)
 V..... vp9_cuvid             (codec vp9)
 V....D h264_qsv              (codec h264)
 V....D hevc_qsv              (codec hevc)
 V....D mpeg2_qsv             (codec mpeg2video)
 V....D vc1_qsv               (codec vc1)
 V....D vp8_qsv               (codec vp8)
```

## HW encoders:
```
 V..... h264_nvenc            (codec h264)
 V..... nvenc                 (codec h264)
 V..... nvenc_h264            (codec h264)
 V..... nvenc_hevc            (codec hevc)
 V..... hevc_nvenc            (codec hevc)
 V..... h264_qsv              (codec h264)
 V..... hevc_qsv              (codec hevc)
 V..... mpeg2_qsv             (codec mpeg2video)
```
## HW scale filters:
```
 ... scale_npp         V->V       (null)
 ... scale_qsv         V->V       (null)
```

## Full Hardware Acceleration Transcode with NVDIA GPU
```
ffmpeg.exe -hwaccel cuvid -c:v h264_cuvid -i <input.mp4> -vf scale_npp=1280:720 -c:v h264_nvenc <output.mp4>
```
> scale_npp only works under x86_64

## H.265 over RTMP
ffmpeg -re -i INPUT -c:v libx265 -tune zerolatency -c:a copy -f flv rtmp://server/live/stream  
Media Server support required. Try this: https://github.com/illuspas/nginx-rtmp-win32/tree/nms  
Client support required. Try this:https://github.com/NodeMedia/NodeMediaClient-Android  
and this:https://github.com/NodeMedia/NodeMediaClient-iOS
