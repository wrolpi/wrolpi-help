# Video Files

WROLPi creates several files when downloading a video:

1. A video file.
2. Caption files. The suffix may be prefixed with the language like so: `.en.vtt` or `.es.vtt`
3. An "info" json file. This file contains large amounts of information about the video: Channel name, Source ID,
   comments, Like count, etc.
4. A poster file (thumbnail).

These files all share the same filename but have different suffixes.

| File Suffix | Purpose                      |
|-------------|------------------------------|
| .mp4        | The video.                   |
| .vtt        | The captions.                |
| .info.json  | Information about the video. |
| .jpg        | The poster (thumbnail).      |

Video files are named using three parts:

1. The Channel Name.
2. The Published Date (upload date).
3. The Source ID (a unique string of characters linking to the video, i.e `0xfMLNVFq2Y`)
4. The title of the video.

The above order is important, it allows the videos to be viewed chronologically in the file browser. The Source ID
is important because it prevents a conflict if a Channel uploads a video with the same name on the same day.

Example file names for a video:

```
/media/videos/wrolpi/WROLPi_20230909_0xfMLNVFq2Y_WROLPi v0.11 beta demo.mp4
/media/videos/wrolpi/WROLPi_20230909_0xfMLNVFq2Y_WROLPi v0.11 beta demo.en.vtt
/media/videos/wrolpi/WROLPi_20230909_0xfMLNVFq2Y_WROLPi v0.11 beta demo.info.json
/media/videos/wrolpi/WROLPi_20230909_0xfMLNVFq2Y_WROLPi v0.11 beta demo.jpg
```