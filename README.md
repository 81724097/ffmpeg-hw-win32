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
> scale_npp only works under x86_64，need to install CUDA_8.0.61, or unzip the npp_dll.zip.

## libx265 10bit
```
ffmpeg.exe -i demo.mp4 -c:v libx265 -pix_fmt yuv420p10 -c:a copy demo_10bit.mp4

........

x265 [info]: HEVC encoder version 2.5
x265 [info]: build info [Windows][GCC 7.2.0][64 bit] 10bit
x265 [info]: using cpu capabilities: MMX2 SSE2Fast LZCNT SSSE3 SSE4.2 AVX FMA3 BMI2 AVX2
x265 [info]: Main 10 profile, Level-2.1 (Main tier)
x265 [info]: Thread pool 0 using 6 threads on numa nodes 0
x265 [info]: Slices                              : 1
x265 [info]: frame threads / pool features       : 2 / wpp(6 rows)
x265 [warning]: Source height < 720p; disabling lookahead-slices
x265 [info]: Coding QT: max CU size, min CU size : 64 / 8
x265 [info]: Residual QT: max TU size, max depth : 32 / 1 inter / 1 intra
x265 [info]: ME / range / subpel / merge         : hex / 57 / 2 / 2
x265 [info]: Keyframe min / max / scenecut / bias: 23 / 250 / 40 / 5.00
x265 [info]: Lookahead / bframes / badapt        : 20 / 4 / 2
x265 [info]: b-pyramid / weightp / weightb       : 1 / 1 / 0
x265 [info]: References / ref-limit  cu / depth  : 3 / on / on
x265 [info]: AQ: mode / str / qg-size / cu-tree  : 1 / 1.0 / 32 / 1
x265 [info]: Rate Control / qCompress            : CRF-28.0 / 0.60
x265 [info]: tools: rd=3 psy-rd=2.00 rskip signhide tmvp strong-intra-smoothing
x265 [info]: tools: deblock sao
```
> libx265 10bit only works under x86_64, need unzip the libx265_main10.zip

## H.265 over RTMP
ffmpeg -re -i INPUT -c:v libx265 -tune zerolatency -c:a copy -f flv rtmp://server/live/stream  
Media Server support required. Try this: https://github.com/illuspas/Node-Media-Server  
Client support required. Try this:https://github.com/NodeMedia/NodeMediaClient-Android  
and this:https://github.com/NodeMedia/NodeMediaClient-iOS
