---
title: "Fix "Adding File Not Supported" Error in WhatsApp Web"
datePublished: Sun Nov 17 2024 10:39:05 GMT+0000 (Coordinated Universal Time)
cuid: cm3lgse4x000l09jt5gl540jr
slug: fix-adding-file-not-supported-error-in-whatsapp-web
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1736405823900/2662f609-4fd8-49c4-83f5-cff423a5edf0.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1736405637127/335db833-435a-4f54-a6b3-bddfc516e01c.png
tags: ffmpeg

---

In what's app web when you upload some video, it shows that **"1 file you tried adding is not supported"**. This is because the video file you are trying to upload does not have correct audio or video codecs.

What's app support, 
- `AAC` or `AC3` audio stream codec and 
- `H264` or `MPEG4` video codec 
- with either `MP4` container or `AVI/MKV` container. 

To fix this you can use some video converter to change codecs to supported codecs. I use `ffmpeg` CLI for this purpose.

```bash
ffmpeg -i input_file -c:v libx264 -c:a aac -strict experimental output_file.mp4

# in case only audio codec need to be changed
ffmpeg -i input_file.mp4 -codec:a aac output_file.mp4
```

## References 

- <https://superuser.com/questions/1216363/whatsapp-doesnt-support-video-format>
