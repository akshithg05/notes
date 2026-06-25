

![[DSA/images/namastedev.com_learn_namaste-frontend-system-design_hld-video-streaming-netflix-hotstar.png]]

Video streaming for different devices might be different protocols. Depending on OS, phone, laptop etc. Its not just the sizing angle.

Other non functional requirements -
- Auth - Limit on the number of devices. Subscription support. (For Netflix)
- SEO - for YouTube this will be important.
- 2 way pagination.

Auth and SEO are covered in other lessons, we can take reference from there.

### 1. Some video terminologies 

|Term|Definition|
|---|---|
|**Adaptive Bitrate Streaming (ABR)**|Automatically switches between video qualities based on network conditions and device capabilities.|
|**Transcoding**|Converting a source video into multiple resolutions, bitrates, and formats for different devices and network speeds.|
|**CDN (Content Delivery Network)**|Distributed network of servers that cache videos closer to users, reducing latency and improving playback performance.|
|**Segment / Chunk**|Small piece of a video file (typically 2–10 seconds) used in streaming protocols like HLS and DASH.|
|**Manifest File**|Metadata file (e.g., `.m3u8`, `.mpd`) listing available video qualities and chunk locations.|
|**Latency**|Time delay between an event occurring and the viewer seeing it. Critical for live streaming.|
|**Caching**|Storing video content temporarily at CDN servers or browsers to reduce repeated downloads.|

For Netflix/YouTube HLD interviews, the most important terms to know well are:

**Streaming → Chunking → Manifest → Adaptive Bitrate Streaming → Transcoding → CDN → Caching → Buffering → Codec.**

These concepts form the backbone of almost every video platform architecture discussion.

Some other terms I came across were - Closed/ open captions - embedded captions in the video cannot be controlled, some we can control playback controls - speed, volumne, quality Seeking - click on any part of the video and video starts from there scrubbing - dragging across the video and seeing the video change as per timestamp manifest file - tells us all the metadata related to the chunk that is actually loaded. Video is fivided into chunks which are independent. These should have info like URL, timestamps,quality of video served for that chunk and resltion subtitle file - srt file - trsnscript with time stamp. ttml - time text markup language - xml format ssc - closed captions webVTT Add these also to the intial tab you gave me

Here's a refined interview-note version with all the terms together:

|Term|Concise Definition|
|---|---|
|**Streaming**|Delivering and playing video in small chunks instead of downloading the entire file first. Playback starts before the full video is received.|
|**Buffering**|Preloading upcoming video chunks into memory before they are needed. Helps prevent playback interruptions caused by network fluctuations.|
|**Bitrate**|Amount of video data transmitted per second (Kbps/Mbps). Higher bitrate generally means better video quality but requires more bandwidth.|
|**Frame Rate (FPS)**|Number of frames displayed per second. Higher FPS results in smoother motion (e.g., 24, 30, 60 FPS).|
|**Resolution**|Number of pixels used to display a video (width × height). Higher resolution generally provides sharper images.|
|**Codec**|Compression/decompression algorithm used to encode and decode video. Examples: H.264, H.265 (HEVC), AV1.|
|**Bandwidth**|Maximum amount of data a network connection can transfer per second. Determines how much video data can be delivered to the viewer.|
|**Poster / Thumbnail**|Static preview image shown before video playback begins. Used to represent and attract users to the content.|
|**Playback Controls**|User controls for interacting with video playback, such as play/pause, volume, speed, quality selection, fullscreen, and subtitles.|
|**Seeking**|Jumping directly to a specific timestamp in a video by clicking or selecting a position on the timeline.|
|**Scrubbing**|Dragging the playback cursor across the timeline while previewing frames at different timestamps.|
|**Open Captions**|Captions permanently embedded into the video frames and cannot be turned on or off by the viewer.|
|**Closed Captions (CC)**|Captions delivered separately from the video and can be enabled, disabled, or customized by the viewer.|
|**Subtitles**|Text version of spoken dialogue, typically intended for translation or language assistance. Usually does not include sound effects.|
|**Manifest File**|Metadata file that describes available video streams, qualities, chunk locations, durations, and bitrates. Used by the player to request video segments.|
|**Segment / Chunk**|Small independent piece of a video (typically 2–10 seconds) that can be downloaded and played separately.|
|**Adaptive Bitrate Streaming (ABR)**|Dynamically switches between video qualities based on available bandwidth and device capabilities.|
|**Transcoding**|Converting a source video into multiple resolutions, bitrates, and formats for different devices and network conditions.|
|**CDN**|Distributed network of servers that cache and deliver video content from locations closer to users.|
|**Caching**|Temporarily storing video content closer to users to reduce latency and improve playback performance.|
|**Latency**|Delay between an event occurring and the viewer seeing it. Particularly important for live streaming.|

### Subtitle / Caption File Formats

|Format|Description|
|---|---|
|**SRT (SubRip Text)**|Most common subtitle format containing text and timestamps. Simple and widely supported.|
|**WebVTT**|Web Video Text Tracks format used by HTML5 video players. Supports styling and positioning.|
|**TTML**|XML-based subtitle and caption format with advanced styling and formatting capabilities.|
|**SCC (Scenarist Closed Captions)**|Industry-standard closed-caption format commonly used in television broadcasting.|

## 2. Frontend Architecture

### Hero Section

- The **Hero Section** is the large banner at the top of the homepage.
- Typically contains an **auto-playing preview video** that should start immediately when the page loads.
- To minimize startup latency, hero content is heavily cached on the client.

### Hero Video Loading Flow

1. User opens Netflix homepage.
2. Backend returns metadata and a short preview video.
3. Video data is received as a **binary payload**.
4. Client converts the binary into a **Blob object**.
5. The Blob is attached to the video player and played immediately.
6. The Blob can be stored in browser cache for future reuse.
7. Cached Blobs can be evicted when no longer needed.

### Blob Usage

- A **Blob (Binary Large Object)** represents binary data such as images, videos, or files.
- Browsers can directly render media from a Blob URL.
- Frequently used for:
    - Hero preview videos
    - Video thumbnails
    - Hover previews
    - Other media assets

### Client-Side Caching

- Caching reduces:
    - Network requests
    - Startup latency
    - Repeated downloads
- Netflix commonly uses **GraphQL + client-side caching** for metadata and UI state.
- Media assets may also be cached locally as Blob objects.

### Thumbnail & Preview Strategy

- Hover previews and thumbnails are often delivered as binary media and converted to Blobs on the client.
- This allows efficient rendering and caching of media assets.

### Netflix Pagination Pattern

Netflix uses **2-dimensional content navigation**:

#### Vertical Pagination

- Scroll through categories/rows.
- Example:
    - Trending Now
    - Action Movies
    - Comedy
    - Continue Watching

#### Horizontal Pagination

- Scroll within a category row.
- Example:
    - Action Movie 1 → Action Movie 2 → Action Movie 3

This creates a **grid of carousels**:

```
Trending Now      → → → →
Action Movies     → → → →
Comedy            → → → →
Continue Watching → → → →
   ↓        ↓
```

### Interview Takeaways

- Hero section must have **low startup latency**.
- Binary media is often converted into **Blob objects** for rendering.
- Client-side caching improves user experience and reduces network calls.
- Netflix UI relies heavily on **horizontal carousels + vertical scrolling**.
- Media previews and thumbnails are optimized for fast loading and caching.

![[DSA/images/namastedev.com_learn_namaste-frontend-system-design_hld-video-streaming-netflix-hotstar.png]]

## 3. Data model

![[Front End System Design/images/namastedev.com_learn_namaste-frontend-system-design_hld-video-streaming-netflix-hotstar 1.png]]


## Video player

1. This is the recommended way of building video player.

![[namastedev.com_learn_namaste-frontend-system-design_hld-video-streaming-netflix-hotstar 1 1.png]]

1. We also have different media and video players to perform these actions.
2. Videojs.com

![[namastedev.com_learn_namaste-frontend-system-design_hld-video-streaming-netflix-hotstar 2.png]]

Using an advanced external web media player (like [Shaka Player](https://www.google.com/url?sa=i&source=web&rct=j&url=https://github.com/shaka-project/shaka-player/issues/1351&ved=2ahUKEwiH8oD6yIOVAxV0UGwGHTZUE94Qy_kOegYIAAgHEAE&opi=89978449&cd&psig=AOvVaw1-Gmcn0wvnnM81gwcJ1PxY&ust=1781417899476000) or [Bitmovin](https://www.google.com/url?sa=i&source=web&rct=j&url=https://bitmovin.com/blog/html5-video-tag-guide/&ved=2ahUKEwiH8oD6yIOVAxV0UGwGHTZUE94Qy_kOegYIAAgHEAI&opi=89978449&cd&psig=AOvVaw1-Gmcn0wvnnM81gwcJ1PxY&ust=1781417899476000)) instead of a basic HTML5 `<video>` tag provides substantial enterprise-level benefits. While the native `<video>` tag is simple to deploy, it lacks the core infrastructure needed for premium streaming platforms. [[1](https://bitmovin.com/blog/html5-video-tag-guide/)]

Based on the presentation in the image, here are the primary reasons to opt for an external media player over a standard video tag:

Advanced Playback Control

- **Automatically jump gaps in content:** Resolves issues with poorly encoded video files or network hiccups by skipping empty data gaps, preventing the video from freezing or buffering indefinitely. [[1](https://github.com/shaka-project/shaka-player/issues/1351)]
- **Pre-Load feature:** Optimizes the user experience by fetching video data in the background before the user hits play, making playback instant.
- **Thumbnails for seeking:** Enables visual preview boxes when a user hovers over or scrubs along the timeline, which is not supported natively by the basic `<video>` tag.
- **Retries:** Configures automated attempts to reconnect and resume playback if a temporary network drop occurs, rather than throwing an immediate error.

Content Security and Offline Capabilities

- **Support for storing content offline:** Allows users to download videos directly within the web environment for later viewing. [[1](https://github.com/shaka-project/shaka-player/issues/1351)]
- **Protected content (DRM) support:** Integrates digital rights management (DRM) like Widevine or FairPlay within offline and online video content to prevent piracy. [[1](https://github.com/shaka-project/shaka-player/issues/1351)]
- **Authentication:** Seamlessly handles user authentication tokens directly inside the video player network layer to ensure only authorized users can pull the video chunks. [[1](https://github.com/shaka-project/shaka-player/issues/1351)]

Streaming and Protocol Support

- **Multi-protocol support (HLS & MSS):** Dynamically switches and plays diverse adaptive streaming formats like Apple's **HLS** (HTTP Live Streaming), Microsoft's **MSS** (Smooth Streaming), or Adobe protocols. A standard video tag cannot natively play these formats without external JavaScript libraries. [[1](https://bitmovin.com/blog/html5-video-tag-guide/), [2](https://github.com/shaka-project/shaka-player/issues/1351)]
- **Network filters:** Allows developers to intercept and modify outgoing video data requests to apply custom headers, proxy settings, or security filters. [[1](https://github.com/shaka-project/shaka-player/issues/1351)]

Ecosystem and Modern Web Integration

- **Cast support:** Built-in integration for casting to external displays like Google Chromecast or smart TVs without writing complex custom API integrations.
- **PWAs & service workers:** Fully optimizes the media architecture to run smoothly within Progressive Web Apps (PWAs), making background downloads and offline availability reliable. [[1](https://github.com/shaka-project/shaka-player/issues/1351)]


![[namastedev.com_learn_namaste-frontend-system-design_hld-video-streaming-netflix-hotstar 3.png]]

![[namastedev.com_learn_namaste-frontend-system-design_hld-video-streaming-netflix-hotstar 1 2.png]]

