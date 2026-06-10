

![[namastedev.com_learn_namaste-frontend-system-design_hld-video-streaming-netflix-hotstar.png]]

Video streaming for different devices might be different protocols. Depending on OS, phone, laptop etc. Its not just the sizing angle.

Other non functional requirements -
- Auth - Limit on the number of devices. Subscription support. (For Netflix)
- SEO - for YouTube this will be important.

Auth and SEO are covered in other lessons, we can take reference from there.

### 1. Some video terminologies 

|Term|Concise Interview Definition|
|---|---|
|**Streaming**|Video is delivered and played in small chunks instead of downloading the entire file first. Playback can begin before the complete video is received.|
|**Buffering**|Preloading upcoming video chunks into memory before they are needed. Helps prevent playback interruptions caused by network fluctuations.|
|**Bitrate**|Amount of video data transmitted per second, usually measured in Kbps or Mbps. Higher bitrate generally produces better visual quality but requires more bandwidth.|
|**Frame Rate (FPS)**|Number of video frames displayed per second. Higher FPS results in smoother motion (e.g., 24 FPS, 30 FPS, 60 FPS).|
|**Resolution**|Number of pixels used to display a video, expressed as width × height (e.g., 1920×1080). Higher resolution generally provides sharper images.|
|**Codec**|Compression/decompression algorithm used to encode video for storage/transmission and decode it for playback. Examples: H.264 (AVC), H.265 (HEVC), AV1.|
|**Bandwidth**|Maximum amount of data that can be transferred over a network connection per second. Determines how much video data can be delivered to the viewer.|
|**Poster / Thumbnail**|Static preview image shown before video playback begins. Used to represent and attract users to the video content.|
