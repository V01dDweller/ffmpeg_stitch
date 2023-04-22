# ffmpeg_stitch

Since the file size limit on my GoPro is 4GB and long videos can exceed 4GB, a
single recording is often split into multiple files. This simple bash script
will concatenate these back into a single file.

## To-Do

Update the script to handle multiple multi-part files automatically to
eliminate the need for manual sorting and directory creation.

## Prerequisites

Install [ffmpeg](https://ffmpeg.org/).

## Installation

Copy `stitch` to a directory in your `PATH`, e.g. `~/.local/bin`.

## Preparation

Copy your GoPro files to a folder on your PC. Consider the list of files
copied from my GoPro:

```txt
GX010076.MP4
GX010077.MP4
GX010078.MP4
GX010079.MP4
GX020076.MP4
GX020078.MP4
GX020079.MP4
GX030076.MP4
GX030078.MP4
GX030079.MP4
GX040076.MP4
GX040078.MP4
GX040079.MP4
GX050076.MP4
GX060076.MP4
GX070076.MP4
GX080076.MP4
```

Using the last two digits of the file names, we can see that there are four
recordings:

- `GX0x0076.MP4`
- `GX010077.MP4`
- `GX0x0078.MP4`
- `GX0x0079.MP4`

Since `GX010077.MP4` was a short recording, there is only one file. However,
the other three were much longer and split into multiple files.

### Step 1

For each multi-part file, create a folder then move the files for that
recording into it, for example:

```txt
├── GX010076
│   ├── GX010076.MP4
│   ├── GX020076.MP4
│   ├── GX030076.MP4
│   ├── GX040076.MP4
│   ├── GX050076.MP4
│   ├── GX060076.MP4
│   ├── GX070076.MP4
│   └── GX080076.MP4
├── GX010077.MP4
├── GX010078
│   ├── GX010078.MP4
│   ├── GX020078.MP4
│   ├── GX030078.MP4
│   └── GX040078.MP4
└── GX010079
    ├── GX010079.MP4
    ├── GX020079.MP4
    ├── GX030079.MP4
    └── GX040079.MP4
```

### Step 2

CD into a folder and run `stitch`, e.g.:

```cmd
cd GX010079
stitch
```

<details>
<summary>Sample output</summary>

```txt
bash-5.0$ cd GX010079

bash-5.0$ ls
GX010079.MP4  GX020079.MP4  GX030079.MP4  GX040079.MP4```

bash-5.0$ stitch
ffmpeg version 4.2.7-0ubuntu0.1 Copyright (c) 2000-2022 the FFmpeg developers
  built with gcc 9 (Ubuntu 9.4.0-1ubuntu1~20.04.1)
  configuration: --prefix=/usr --extra-version=0ubuntu0.1 --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --arch=amd64 --enable-gpl --disable-stripping --enable-avresample --disable-filter=resample --enable-avisynth --enable-gnutls --enable-ladspa --enable-libaom --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libcodec2 --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libjack --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librsvg --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzmq --enable-libzvbi --enable-lv2 --enable-omx --enable-openal --enable-opencl --enable-opengl --enable-sdl2 --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-nvenc --enable-chromaprint --enable-frei0r --enable-libx264 --enable-shared
  libavutil      56. 31.100 / 56. 31.100
  libavcodec     58. 54.100 / 58. 54.100
  libavformat    58. 29.100 / 58. 29.100
  libavdevice    58.  8.100 / 58.  8.100
  libavfilter     7. 57.100 /  7. 57.100
  libavresample   4.  0.  0 /  4.  0.  0
  libswscale      5.  5.100 /  5.  5.100
  libswresample   3.  5.100 /  3.  5.100
  libpostproc    55.  5.100 / 55.  5.100
[mov,mp4,m4a,3gp,3g2,mj2 @ 0x5651ff24f700] Using non-standard frame rate 59/1
[concat @ 0x5651ff245340] Could not find codec parameters for stream 2 (Unknown: none): unknown codec
Consider increasing the value for the 'analyzeduration' and 'probesize' options
Input #0, concat, from 'files.txt':
  Duration: N/A, start: 0.000000, bitrate: 59933 kb/s
    Stream #0:0(eng): Video: hevc (Main) (hvc1 / 0x31637668), yuvj420p(pc, bt709), 3840x2160 [SAR 1:1 DAR 16:9], 59688 kb/s, 59.94 fps, 59.94 tbr, 60k tbn, 59.94 tbc
    Metadata:
      creation_time   : 2023-02-18T11:40:56.000000Z
      handler_name    : GoPro H.265
      encoder         : GoPro H.265 encoder
      timecode        : 11:52:06:57
    Stream #0:1(eng): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 189 kb/s
    Metadata:
      creation_time   : 2023-02-18T11:40:56.000000Z
      handler_name    : GoPro AAC
      timecode        : 11:52:06:57
    Stream #0:2: Unknown: none
    Stream #0:3(eng): Data: bin_data (gpmd / 0x646D7067), 56 kb/s
    Metadata:
      creation_time   : 2023-02-18T11:40:56.000000Z
      handler_name    : GoPro MET
Output #0, mp4, to 'final.mp4':
  Metadata:
    encoder         : Lavf58.29.100
    Stream #0:0(eng): Video: hevc (Main) (hvc1 / 0x31637668), yuvj420p(pc, bt709), 3840x2160 [SAR 1:1 DAR 16:9], q=2-31, 59688 kb/s, 0.02 fps, 59.94 tbr, 60k tbn, 60k tbc
    Metadata:
      creation_time   : 2023-02-18T11:40:56.000000Z
      handler_name    : GoPro H.265
      encoder         : GoPro H.265 encoder
      timecode        : 11:52:06:57
    Stream #0:1(eng): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 189 kb/s
    Metadata:
      creation_time   : 2023-02-18T11:40:56.000000Z
      handler_name    : GoPro AAC
      timecode        : 11:52:06:57
Stream mapping:
  Stream #0:0 -> #0:0 (copy)
  Stream #0:1 -> #0:1 (copy)
Press [q] to stop, [?] for help
frame=  826 fps=0.0 q=-1.0 size=  100864kB time=00:00:13.76 bitrate=60032.9kbits/s speed=27.5x frame= 1511 fps=1510 q=-1.0 size=  184064kB time=00:00:25.19 bitrate=59854.8kbits/s speed=25.2xframe= 2210 fps=1473 q=-1.0 size=  269568kB time=00:00:36.85 bitrate=59921.1kbits/s speed=24.6xframe= 2906 fps=1452 q=-1.0 size=  354560kB time=00:00:48.46 bitrate=59925.6kbits/s speed=24.2xframe= 3490 fps=1395 q=-1.0 size=  425728kB time=00:00:58.20 bitrate=59915.4kbits/s speed=23.3xframe= 3971 fps=1323 q=-1.0 size=  484608kB time=00:01:06.24 bitrate=59932.2kbits/s speed=22.1xframe= 4459 fps=1273 q=-1.0 size=  543744kB time=00:01:14.37 bitrate=59891.0kbits/s speed=21.2xframe= 4917 fps=1229 q=-1.0 size=  599552kB time=00:01:22.02 bitrate=59877.2kbits/s speed=20.5xframe= 5376 fps=1194 q=-1.0 size=  655616kB time=00:01:29.67 bitrate=59893.3kbits/s speed=19.9xframe= 5847 fps=1169 q=-1.0 size=  713216kB time=00:01:37.53 bitrate=59905.9kbits/s speed=19.5xframe= 6311 fps=1147 q=-1.0 size=  769280kB time=00:01:45.27 bitrate=59863.5kbits/s speed=19.1xframe= 6811 fps=1134 q=-1.0 size=  830720kB time=00:01:53.62 bitrate=59894.2kbits/s speed=18.9xframe= 7248 fps=1114 q=-1.0 size=  883968kB time=00:02:00.90 bitrate=59894.3kbits/s speed=18.6xframe= 7710 fps=1101 q=-1.0 size=  940288kB time=00:02:08.61 bitrate=59889.0kbits/s speed=18.4xframe= 8158 fps=1087 q=-1.0 size=  994816kB time=00:02:16.08 bitrate=59885.2kbits/s speed=18.1xframe= 8569 fps=1070 q=-1.0 size= 1044992kB time=00:02:22.94 bitrate=59888.1kbits/s speed=17.9xframe= 9031 fps=1062 q=-1.0 size= 1101312kB time=00:02:30.65 bitrate=59886.6kbits/s speed=17.7xframe= 9476 fps=1052 q=-1.0 size= 1155328kB time=00:02:38.07 bitrate=59873.3kbits/s speed=17.5xframe= 9915 fps=1043 q=-1.0 size= 1209088kB time=00:02:45.39 bitrate=59884.7kbits/s speed=17.4xframe=10413 fps=1041 q=-1.0 size= 1270016kB time=00:02:53.71 bitrate=59890.2kbits/s speed=17.4xframe=10928 fps=1040 q=-1.0 size= 1332224kB time=00:03:02.31 bitrate=59861.2kbits/s speed=17.4xframe=11418 fps=1037 q=-1.0 size= 1392384kB time=00:03:10.47 bitrate=59884.5kbits/s speed=17.3xframe=11928 fps=1036 q=-1.0 size= 1455104kB time=00:03:18.98 bitrate=59905.9kbits/s speed=17.3xframe=12435 fps=1035 q=-1.0 size= 1517312kB time=00:03:27.44 bitrate=59918.5kbits/s speed=17.3xframe=12934 fps=1034 q=-1.0 size= 1577216kB time=00:03:35.76 bitrate=59882.4kbits/s speed=17.2xframe=13416 fps=1031 q=-1.0 size= 1636352kB time=00:03:43.80 bitrate=59895.4kbits/s speed=17.2xframe=13891 fps=1028 q=-1.0 size= 1694208kB time=00:03:51.74 bitrate=59889.2kbits/s speed=17.2xframe=14395 fps=1027 q=-1.0 size= 1755392kB time=00:04:00.14 bitrate=59880.1kbits/s speed=17.1xframe=14881 fps=1025 q=-1.0 size= 1815040kB time=00:04:08.25 bitrate=59893.0kbits/s speed=17.1xframe=15334 fps=1021 q=-1.0 size= 1870336kB time=00:04:15.80 bitrate=59895.7kbits/s speed=  17xframe=15800 fps=1019 q=-1.0 size= 1927168kB time=00:04:23.58 bitrate=59895.9kbits/s speed=  17xframe=16293 fps=1018 q=-1.0 size= 1987072kB time=00:04:31.80 bitrate=59888.2kbits/s speed=  17xframe=16773 fps=1016 q=-1.0 size= 2045184kB time=00:04:39.82 bitrate=59872.7kbits/s speed=16.9xframe=17240 fps=1013 q=-1.0 size= 2102272kB time=00:04:47.61 bitrate=59877.8kbits/s speed=16.9xframe=17679 fps=1009 q=-1.0 size= 2156032kB time=00:04:54.93 bitrate=59885.4kbits/s speed=16.8xframe=18162 fps=1008 q=-1.0 size= 2215168kB time=00:05:02.98 bitrate=59892.7kbits/s speed=16.8xframe=18643 fps=1007 q=-1.0 size= 2273792kB time=00:05:11.01 bitrate=59891.5kbits/s speed=16.8xframe=19057 fps=1002 q=-1.0 size= 2324224kB time=00:05:17.91 bitrate=59889.9kbits/s speed=16.7xframe=19534 fps=1001 q=-1.0 size= 2382336kB time=00:05:25.88 bitrate=59885.9kbits/s speed=16.7xframe=20033 fps=1001 q=-1.0 size= 2443264kB time=00:05:34.20 bitrate=59888.5kbits/s speed=16.7xframe=20467 fps=998 q=-1.0 size= 2496256kB time=00:05:41.44 bitrate=59891.2kbits/s speed=16.6x frame=20947 fps=997 q=-1.0 size= 2554368kB time=00:05:49.44 bitrate=59881.1kbits/s speed=16.6x frame=21427 fps=996 q=-1.0 size= 2613248kB time=00:05:57.46 bitrate=59888.2kbits/s speed=16.6x frame=21948 fps=997 q=-1.0 size= 2676992kB time=00:06:06.14 bitrate=59893.4kbits/s speed=16.6x frame=22473 fps=998 q=-1.0 size= 2741248kB time=00:06:14.91 bitrate=59897.5kbits/s speed=16.6x frame=22988 fps=999 q=-1.0 size= 2803712kB time=00:06:23.49 bitrate=59890.5kbits/s speed=16.7x frame=23508 fps=1000 q=-1.0 size= 2867200kB time=00:06:32.17 bitrate=59891.9kbits/s speed=16.7xframe=23991 fps=999 q=-1.0 size= 2925824kB time=00:06:40.23 bitrate=59886.0kbits/s speed=16.7x frame=24434 fps=997 q=-1.0 size= 2979840kB time=00:06:47.62 bitrate=59885.7kbits/s speed=16.6x frame=24922 fps=996 q=-1.0 size= 3039232kB time=00:06:55.76 bitrate=59883.3kbits/s speed=16.6x frame=25408 fps=996 q=-1.0 size= 3098112kB time=00:07:03.87 bitrate=59875.7kbits/s speed=16.6x frame=25863 fps=994 q=-1.0 size= 3154432kB time=00:07:11.46 bitrate=59891.3kbits/s speed=16.6x frame=26381 fps=995 q=-1.0 size= 3216896kB time=00:07:20.10 bitrate=59878.3kbits/s speed=16.6x frame=26874 fps=995 q=-1.0 size= 3277824kB time=00:07:28.33 bitrate=59893.1kbits/s speed=16.6x frame=27392 fps=995 q=-1.0 size= 3340800kB time=00:07:36.97 bitrate=59889.4kbits/s speed=16.6x frame=27906 fps=996 q=-1.0 size= 3403520kB time=00:07:45.54 bitrate=59889.9kbits/s speed=16.6x frame=28400 fps=996 q=-1.0 size= 3463680kB time=00:07:53.79 bitrate=59888.0kbits/s speed=16.6x frame=28919 fps=996 q=-1.0 size= 3526912kB time=00:08:02.45 bitrate=59886.5kbits/s speed=16.6x frame=29459 fps=998 q=-1.0 size= 3592448kB time=00:08:11.45 bitrate=59881.7kbits/s speed=16.6x frame=29960 fps=998 q=-1.0 size= 3653632kB time=00:08:19.81 bitrate=59883.1kbits/s speed=16.6x frame=30466 fps=998 q=-1.0 size= 3715840kB time=00:08:28.25 bitrate=59891.2kbits/s speed=16.7x frame=30961 fps=998 q=-1.0 size= 3776256kB time=00:08:36.52 bitrate=59891.1kbits/s speed=16.6x frame=31424 fps=997 q=-1.0 size= 3832320kB time=00:08:44.24 bitrate=59885.4kbits/s speed=16.6x frame=31891 fps=996 q=-1.0 size= 3889408kB time=00:08:52.03 bitrate=59887.4kbits/s speed=16.6x [mov,mp4,m4a,3gp,3g2,mj2 @ 0x5651ff251d40] Using non-standard frame rate 59/1
frame=32363 fps=995 q=-1.0 size= 3947264kB time=00:08:59.92 bitrate=59890.2kbits/s speed=16.6x frame=32907 fps=996 q=-1.0 size= 4013312kB time=00:09:08.99 bitrate=59885.7kbits/s speed=16.6x frame=33395 fps=996 q=-1.0 size= 4072960kB time=00:09:17.13 bitrate=59887.6kbits/s speed=16.6x frame=33817 fps=994 q=-1.0 size= 4124160kB time=00:09:24.17 bitrate=59883.7kbits/s speed=16.6x frame=34274 fps=993 q=-1.0 size= 4179968kB time=00:09:31.80 bitrate=59884.8kbits/s speed=16.6x frame=34796 fps=993 q=-1.0 size= 4243456kB time=00:09:40.51 bitrate=59882.3kbits/s speed=16.6x frame=35283 fps=993 q=-1.0 size= 4302848kB time=00:09:48.63 bitrate=59882.3kbits/s speed=16.6x frame=35807 fps=994 q=-1.0 size= 4366336kB time=00:09:57.37 bitrate=59876.6kbits/s speed=16.6x frame=36237 fps=992 q=-1.0 size= 4419328kB time=00:10:04.55 bitrate=59884.2kbits/s speed=16.5x frame=36725 fps=992 q=-1.0 size= 4479232kB time=00:10:12.69 bitrate=59889.4kbits/s speed=16.5x frame=37240 fps=992 q=-1.0 size= 4541184kB time=00:10:21.28 bitrate=59878.0kbits/s speed=16.6x frame=37746 fps=992 q=-1.0 size= 4603392kB time=00:10:29.72 bitrate=59884.6kbits/s speed=16.6x frame=38256 fps=993 q=-1.0 size= 4665344kB time=00:10:38.23 bitrate=59881.4kbits/s speed=16.6x frame=38765 fps=993 q=-1.0 size= 4727808kB time=00:10:46.72 bitrate=59886.4kbits/s speed=16.6x frame=39233 fps=992 q=-1.0 size= 4784640kB time=00:10:54.53 bitrate=59883.3kbits/s speed=16.6x frame=39708 fps=992 q=-1.0 size= 4842752kB time=00:11:02.46 bitrate=59885.6kbits/s speed=16.5x frame=40211 fps=992 q=-1.0 size= 4904192kB time=00:11:10.85 bitrate=59886.7kbits/s speed=16.5x frame=40701 fps=992 q=-1.0 size= 4963328kB time=00:11:19.02 bitrate=59879.2kbits/s speed=16.5x frame=41218 fps=992 q=-1.0 size= 5026560kB time=00:11:27.65 bitrate=59881.4kbits/s speed=16.6x frame=41710 fps=992 q=-1.0 size= 5086720kB time=00:11:35.86 bitrate=59883.3kbits/s speed=16.6x frame=42219 fps=993 q=-1.0 size= 5148928kB time=00:11:44.35 bitrate=59884.8kbits/s speed=16.6x frame=42732 fps=993 q=-1.0 size= 5211392kB time=00:11:52.91 bitrate=59883.7kbits/s speed=16.6x frame=43197 fps=992 q=-1.0 size= 5267456kB time=00:12:00.66 bitrate=59876.3kbits/s speed=16.6x frame=43668 fps=992 q=-1.0 size= 5325568kB time=00:12:08.52 bitrate=59884.0kbits/s speed=16.5x frame=44114 fps=990 q=-1.0 size= 5380096kB time=00:12:15.96 bitrate=59885.5kbits/s speed=16.5x frame=44545 fps=989 q=-1.0 size= 5432576kB time=00:12:23.15 bitrate=59884.5kbits/s speed=16.5x frame=45038 fps=989 q=-1.0 size= 5492480kB time=00:12:31.38 bitrate=59882.1kbits/s speed=16.5x frame=45485 fps=988 q=-1.0 size= 5546752kB time=00:12:38.84 bitrate=59879.5kbits/s speed=16.5x frame=45924 fps=987 q=-1.0 size= 5600768kB time=00:12:46.16 bitrate=59884.6kbits/s speed=16.5x frame=46385 fps=986 q=-1.0 size= 5656576kB time=00:12:53.85 bitrate=59880.3kbits/s speed=16.5x frame=46817 fps=985 q=-1.0 size= 5709568kB time=00:13:01.06 bitrate=59883.5kbits/s speed=16.4x frame=47285 fps=984 q=-1.0 size= 5766656kB time=00:13:08.87 bitrate=59883.7kbits/s speed=16.4x frame=47752 fps=984 q=-1.0 size= 5823488kB time=00:13:16.66 bitrate=59882.4kbits/s speed=16.4x frame=48258 fps=984 q=-1.0 size= 5884160kB time=00:13:25.10 bitrate=59871.9kbits/s speed=16.4x frame=48787 fps=985 q=-1.0 size= 5949440kB time=00:13:33.92 bitrate=59879.7kbits/s speed=16.4x frame=49285 fps=985 q=-1.0 size= 6010624kB time=00:13:42.23 bitrate=59884.3kbits/s speed=16.4x frame=49805 fps=985 q=-1.0 size= 6074112kB time=00:13:50.91 bitrate=59884.9kbits/s speed=16.4x frame=50344 fps=986 q=-1.0 size= 6139648kB time=00:13:59.90 bitrate=59883.0kbits/s speed=16.5x frame=50849 fps=987 q=-1.0 size= 6201088kB time=00:14:08.32 bitrate=59881.6kbits/s speed=16.5x frame=51349 fps=987 q=-1.0 size= 6262016kB time=00:14:16.67 bitrate=59881.1kbits/s speed=16.5x frame=51823 fps=986 q=-1.0 size= 6320384kB time=00:14:24.57 bitrate=59886.5kbits/s speed=16.5x frame=52280 fps=986 q=-1.0 size= 6375680kB time=00:14:32.20 bitrate=59882.3kbits/s speed=16.4x frame=52744 fps=985 q=-1.0 size= 6432512kB time=00:14:39.94 bitrate=59884.6kbits/s speed=16.4x frame=53217 fps=985 q=-1.0 size= 6488832kB time=00:14:47.83 bitrate=59872.0kbits/s speed=16.4x frame=53637 fps=983 q=-1.0 size= 6541056kB time=00:14:54.84 bitrate=59881.3kbits/s speed=16.4x frame=54070 fps=982 q=-1.0 size= 6594048kB time=00:15:02.06 bitrate=59883.0kbits/s speed=16.4x frame=54511 fps=981 q=-1.0 size= 6648064kB time=00:15:09.42 bitrate=59885.1kbits/s speed=16.4x frame=54931 fps=980 q=-1.0 size= 6698496kB time=00:15:16.43 bitrate=59878.0kbits/s speed=16.4x frame=55390 fps=980 q=-1.0 size= 6754816kB time=00:15:24.08 bitrate=59881.1kbits/s speed=16.3x frame=55836 fps=979 q=-1.0 size= 6809600kB time=00:15:31.52 bitrate=59884.6kbits/s speed=16.3x frame=56313 fps=979 q=-1.0 size= 6867712kB time=00:15:39.48 bitrate=59884.0kbits/s speed=16.3x frame=56786 fps=978 q=-1.0 size= 6924544kB time=00:15:47.37 bitrate=59876.7kbits/s speed=16.3x frame=57254 fps=978 q=-1.0 size= 6981888kB time=00:15:55.18 bitrate=59879.0kbits/s speed=16.3x frame=57754 fps=978 q=-1.0 size= 7043840kB time=00:16:03.52 bitrate=59887.4kbits/s speed=16.3x frame=58294 fps=979 q=-1.0 size= 7109888kB time=00:16:12.53 bitrate=59888.9kbits/s speed=16.3x frame=58826 fps=980 q=-1.0 size= 7173888kB time=00:16:21.41 bitrate=59881.5kbits/s speed=16.3x frame=59386 fps=981 q=-1.0 size= 7243008kB time=00:16:30.75 bitrate=59888.4kbits/s speed=16.4x frame=59934 fps=982 q=-1.0 size= 7309312kB time=00:16:39.89 bitrate=59884.0kbits/s speed=16.4x frame=60477 fps=983 q=-1.0 size= 7375360kB time=00:16:48.95 bitrate=59882.6kbits/s speed=16.4x frame=61035 fps=984 q=-1.0 size= 7443712kB time=00:16:58.26 bitrate=59885.0kbits/s speed=16.4x frame=61545 fps=984 q=-1.0 size= 7505920kB time=00:17:06.77 bitrate=59885.1kbits/s speed=16.4x frame=62088 fps=985 q=-1.0 size= 7572736kB time=00:17:15.83 bitrate=59889.8kbits/s speed=16.4x frame=62594 fps=985 q=-1.0 size= 7633152kB time=00:17:24.27 bitrate=59879.6kbits/s speed=16.4x frame=63082 fps=985 q=-1.0 size= 7693056kB time=00:17:32.41 bitrate=59882.7kbits/s speed=16.4x frame=63627 fps=986 q=-1.0 size= 7759616kB time=00:17:41.50 bitrate=59883.4kbits/s speed=16.4x [mov,mp4,m4a,3gp,3g2,mj2 @ 0x5651ff251d40] Using non-standard frame rate 59/1
frame=64106 fps=985 q=-1.0 size= 7817984kB time=00:17:49.50 bitrate=59883.0kbits/s speed=16.4x frame=64590 fps=985 q=-1.0 size= 7877120kB time=00:17:57.57 bitrate=59883.9kbits/s speed=16.4x frame=65101 fps=986 q=-1.0 size= 7938560kB time=00:18:06.10 bitrate=59877.2kbits/s speed=16.4x frame=65623 fps=986 q=-1.0 size= 8003072kB time=00:18:14.80 bitrate=59883.7kbits/s speed=16.4x frame=66151 fps=986 q=-1.0 size= 8067840kB time=00:18:23.62 bitrate=59886.2kbits/s speed=16.5x frame=66659 fps=987 q=-1.0 size= 8129792kB time=00:18:32.09 bitrate=59886.4kbits/s speed=16.5x frame=67158 fps=987 q=-1.0 size= 8190208kB time=00:18:40.41 bitrate=59883.2kbits/s speed=16.5x frame=67681 fps=987 q=-1.0 size= 8253952kB time=00:18:49.14 bitrate=59882.9kbits/s speed=16.5x frame=68220 fps=988 q=-1.0 size= 8319744kB time=00:18:58.13 bitrate=59883.1kbits/s speed=16.5x frame=68729 fps=988 q=-1.0 size= 8381696kB time=00:19:06.62 bitrate=59882.4kbits/s speed=16.5x frame=69272 fps=989 q=-1.0 size= 8448768kB time=00:19:15.68 bitrate=59888.5kbits/s speed=16.5x frame=69837 fps=990 q=-1.0 size= 8516864kB time=00:19:25.11 bitrate=59882.8kbits/s speed=16.5x frame=70356 fps=990 q=-1.0 size= 8580608kB time=00:19:33.77 bitrate=59885.9kbits/s speed=16.5x frame=70907 fps=991 q=-1.0 size= 8648192kB time=00:19:42.96 bitrate=59888.6kbits/s speed=16.5x frame=71446 fps=991 q=-1.0 size= 8713472kB time=00:19:51.95 bitrate=59885.4kbits/s speed=16.5x frame=72031 fps=993 q=-1.0 size= 8784128kB time=00:20:01.71 bitrate=59880.7kbits/s speed=16.6x frame=72595 fps=994 q=-1.0 size= 8854272kB time=00:20:11.12 bitrate=59889.9kbits/s speed=16.6x frame=73106 fps=994 q=-1.0 size= 8915456kB time=00:20:19.65 bitrate=59882.3kbits/s speed=16.6x frame=73606 fps=994 q=-1.0 size= 8976640kB time=00:20:27.99 bitrate=59883.6kbits/s speed=16.6x frame=74134 fps=994 q=-1.0 size= 9041408kB time=00:20:36.80 bitrate=59885.9kbits/s speed=16.6x frame=74597 fps=994 q=-1.0 size= 9097472kB time=00:20:44.52 bitrate=59883.3kbits/s speed=16.6x frame=75102 fps=994 q=-1.0 size= 9159168kB time=00:20:52.95 bitrate=59884.2kbits/s speed=16.6x frame=75579 fps=994 q=-1.0 size= 9217792kB time=00:21:00.91 bitrate=59886.9kbits/s speed=16.6x frame=76110 fps=994 q=-1.0 size= 9281792kB time=00:21:09.76 bitrate=59882.2kbits/s speed=16.6x frame=76623 fps=994 q=-1.0 size= 9345024kB time=00:21:18.32 bitrate=59886.5kbits/s speed=16.6x frame=77114 fps=994 q=-1.0 size= 9404160kB time=00:21:26.51 bitrate=59881.7kbits/s speed=16.6x frame=77617 fps=994 q=-1.0 size= 9466112kB time=00:21:34.90 bitrate=59885.6kbits/s speed=16.6x frame=78121 fps=994 q=-1.0 size= 9527808kB time=00:21:43.32 bitrate=59886.8kbits/s speed=16.6x frame=78593 fps=994 q=-1.0 size= 9584640kB time=00:21:51.19 bitrate=59882.4kbits/s speed=16.6x frame=79093 fps=994 q=-1.0 size= 9645568kB time=00:21:59.53 bitrate=59882.1kbits/s speed=16.6x frame=79603 fps=994 q=-1.0 size= 9708288kB time=00:22:08.04 bitrate=59885.4kbits/s speed=16.6x frame=80092 fps=994 q=-1.0 size= 9767680kB time=00:22:16.20 bitrate=59883.9kbits/s speed=16.6x frame=80612 fps=994 q=-1.0 size= 9831424kB time=00:22:24.87 bitrate=59885.9kbits/s speed=16.6x frame=81066 fps=994 q=-1.0 size= 9886720kB time=00:22:32.44 bitrate=59885.4kbits/s speed=16.6x frame=81588 fps=994 q=-1.0 size= 9949952kB time=00:22:41.15 bitrate=59882.8kbits/s speed=16.6x frame=82085 fps=994 q=-1.0 size=10010880kB time=00:22:49.45 bitrate=59884.7kbits/s speed=16.6x frame=82575 fps=994 q=-1.0 size=10070272kB time=00:22:57.62 bitrate=59882.5kbits/s speed=16.6x frame=83089 fps=994 q=-1.0 size=10133248kB time=00:23:06.20 bitrate=59884.1kbits/s speed=16.6x frame=83599 fps=994 q=-1.0 size=10195200kB time=00:23:14.71 bitrate=59882.5kbits/s speed=16.6x frame=84081 fps=994 q=-1.0 size=10254080kB time=00:23:22.75 bitrate=59883.4kbits/s speed=16.6x frame=84535 fps=994 q=-1.0 size=10309120kB time=00:23:30.33 bitrate=59881.2kbits/s speed=16.6x frame=84955 fps=993 q=-1.0 size=10360576kB time=00:23:37.33 bitrate=59882.9kbits/s speed=16.6x frame=85358 fps=992 q=-1.0 size=10409728kB time=00:23:44.05 bitrate=59882.9kbits/s speed=16.5x frame=85763 fps=991 q=-1.0 size=10459136kB time=00:23:50.81 bitrate=59883.0kbits/s speed=16.5x frame=86152 fps=989 q=-1.0 size=10507008kB time=00:23:57.30 bitrate=59885.4kbits/s speed=16.5x frame=86604 fps=989 q=-1.0 size=10561792kB time=00:24:04.84 bitrate=59883.5kbits/s speed=16.5x frame=87122 fps=989 q=-1.0 size=10625280kB time=00:24:13.48 bitrate=59885.3kbits/s speed=16.5x frame=87578 fps=989 q=-1.0 size=10680832kB time=00:24:21.09 bitrate=59884.9kbits/s speed=16.5x frame=88056 fps=989 q=-1.0 size=10739200kB time=00:24:29.06 bitrate=59885.3kbits/s speed=16.5x frame=88528 fps=988 q=-1.0 size=10796288kB time=00:24:36.94 bitrate=59882.7kbits/s speed=16.5x frame=88905 fps=987 q=-1.0 size=10842368kB time=00:24:43.23 bitrate=59883.3kbits/s speed=16.5x frame=89297 fps=986 q=-1.0 size=10890240kB time=00:24:49.77 bitrate=59883.4kbits/s speed=16.4x frame=89675 fps=985 q=-1.0 size=10936320kB time=00:24:56.07 bitrate=59883.5kbits/s speed=16.4x frame=90071 fps=984 q=-1.0 size=10984960kB time=00:25:02.68 bitrate=59885.4kbits/s speed=16.4x frame=90500 fps=983 q=-1.0 size=11036928kB time=00:25:09.84 bitrate=59883.5kbits/s speed=16.4x frame=90869 fps=982 q=-1.0 size=11081728kB time=00:25:15.99 bitrate=59882.4kbits/s speed=16.4x frame=91252 fps=980 q=-1.0 size=11128832kB time=00:25:22.38 bitrate=59884.5kbits/s speed=16.4x frame=91618 fps=979 q=-1.0 size=11173632kB time=00:25:28.49 bitrate=59885.2kbits/s speed=16.3x frame=91969 fps=978 q=-1.0 size=11216384kB time=00:25:34.34 bitrate=59885.1kbits/s speed=16.3x frame=92276 fps=976 q=-1.0 size=11253504kB time=00:25:39.46 bitrate=59883.4kbits/s speed=16.3x frame=92510 fps=973 q=-1.0 size=11281664kB time=00:25:43.37 bitrate=59881.4kbits/s speed=16.2x frame=92770 fps=971 q=-1.0 size=11313920kB time=00:25:47.71 bitrate=59884.3kbits/s speed=16.2x frame=93082 fps=969 q=-1.0 size=11352064kB time=00:25:52.91 bitrate=59884.8kbits/s speed=16.2x frame=93423 fps=967 q=-1.0 size=11393280kB time=00:25:58.60 bitrate=59882.8kbits/s speed=16.1x frame=93738 fps=966 q=-1.0 size=11431936kB time=00:26:03.86 bitrate=59884.1kbits/s speed=16.1x frame=94078 fps=964 q=-1.0 size=11473664kB time=00:26:09.53 bitrate=59885.5kbits/s speed=16.1x frame=94398 fps=962 q=-1.0 size=11512832kB time=00:26:14.87 bitrate=59886.1kbits/s speed=16.1x frame=94712 fps=961 q=-1.0 size=11550976kB time=00:26:20.11 bitrate=59885.4kbits/s speed=  16x frame=94984 fps=959 q=-1.0 size=11583744kB time=00:26:24.64 bitrate=59883.3kbits/s speed=  16x frame=95271 fps=957 q=-1.0 size=11618560kB time=00:26:29.43 bitrate=59882.4kbits/s speed=  16x frame=95549 fps=955 q=-1.0 size=11651840kB time=00:26:34.07 bitrate=59879.1kbits/s speed=15.9x frame=95851 fps=953 q=-1.0 size=11689728kB time=00:26:39.11 bitrate=59884.6kbits/s speed=15.9x [mov,mp4,m4a,3gp,3g2,mj2 @ 0x5651ff267800] Using non-standard frame rate 59/1
frame=96166 fps=951 q=-1.0 size=11727872kB time=00:26:44.36 bitrate=59883.2kbits/s speed=15.9x frame=96581 fps=951 q=-1.0 size=11778816kB time=00:26:51.29 bitrate=59884.9kbits/s speed=15.9x frame=96954 fps=950 q=-1.0 size=11824640kB time=00:26:57.51 bitrate=59886.6kbits/s speed=15.8x frame=97306 fps=949 q=-1.0 size=11867136kB time=00:27:03.38 bitrate=59884.4kbits/s speed=15.8x frame=97617 fps=947 q=-1.0 size=11905280kB time=00:27:08.57 bitrate=59885.4kbits/s speed=15.8x frame=97994 fps=946 q=-1.0 size=11951104kB time=00:27:14.86 bitrate=59884.7kbits/s speed=15.8x frame=98462 fps=946 q=-1.0 size=12008192kB time=00:27:22.67 bitrate=59884.8kbits/s speed=15.8x frame=98953 fps=946 q=-1.0 size=12068608kB time=00:27:30.87 bitrate=59887.2kbits/s speed=15.8x frame=99382 fps=946 q=-1.0 size=12120064kB time=00:27:38.02 bitrate=59883.2kbits/s speed=15.8x frame=99829 fps=945 q=-1.0 size=12174848kB time=00:27:45.48 bitrate=59884.3kbits/s speed=15.8x frame=100257 fps=945 q=-1.0 size=12227072kB time=00:27:52.63 bitrate=59884.2kbits/s speed=15.8xframe=100733 fps=945 q=-1.0 size=12284928kB time=00:28:00.56 bitrate=59883.7kbits/s speed=15.8xframe=101194 fps=945 q=-1.0 size=12341504kB time=00:28:08.25 bitrate=59885.4kbits/s speed=15.8xframe=101574 fps=944 q=-1.0 size=12387584kB time=00:28:14.59 bitrate=59884.1kbits/s speed=15.7xframe=101940 fps=943 q=-1.0 size=12432640kB time=00:28:20.70 bitrate=59885.9kbits/s speed=15.7xframe=102291 fps=942 q=-1.0 size=12475392kB time=00:28:26.55 bitrate=59885.9kbits/s speed=15.7xframe=102473 fps=941 q=-1.0 Lsize=12500090kB time=00:28:29.58 bitrate=59897.8kbits/s speed=15.7x
video:12458079kB audio:39515kB subtitle:0kB other streams:0kB global headers:0kB muxing overhead: 0.019973%

bash-5.0$ ls
GX010079.MP4  GX020079.MP4  GX030079.MP4  GX040079.MP4  final.mp4
```
</details>

A new file named `final.mp4` will be created. Repeat for each folder.

[modeline]: # ( vi: set textwidth=78 colorcolumn=80: )
