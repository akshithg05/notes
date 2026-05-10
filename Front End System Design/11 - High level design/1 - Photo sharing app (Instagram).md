
1. Do not blindly read from book / notes / videos. We need to understand the expectation of the interviewer and understand the question well.

2. Feel free to ask the interviewer what the application does, what are the features and what are the expectations, if you haven't worked on the application before.

### 1. Problem statement for instagram

#### Categorize into 2 -

1.Functional requirement -

2.Non functional requirement.

(No coding involved)

![[Front End System Design/images/namastedev.com_learn_namaste-frontend-system-design_hld-photo-sharing-app-instagram 3.png]]


### 2. Architecture design

Views - What you see. Eg - Lists, creation
Controller - Consists of the main business logic of our application. How our views are powered. Eg- Filtering, Editing, Upload. (All these can be used for posts, reels and stories, common logic).

Then we can have specific controllers like - PostListing, ReelsListing, StoryListing, PostCreation.

**Note**: - Sometimes we are from different backgrounds (React, Angular, Vue). Try to be generic, do not be specific like useEffect or useState. Try to use terms like controllers and Views instead.

![[namastedev.com_learn_namaste-frontend-system-design_hld-photo-sharing-app-instagram 2 1.png]]

This is enough for anyone who is a mid-range software engineer.

Try to also talk about microservices. How client interacts with upstream layers and projects.
For a small scale application, we can make an API call from the UI itself to the backend and get data and use it. For a large scale application we will need many services for processing the data and to act as a middleware to polish and massage the data used by the UI.


[[2026-05-07]]

![[Front End System Design/images/namastedev.com_learn_namaste-frontend-system-design_hld-photo-sharing-app-instagram 3.png]]

We can have n number of services for n number of applications. 
Examples - 
1. For uploading pictures, post creation, feed service

#### We can have API gateway to route requests.

Depending on request the API gateway will route request to the designated service.

Some of the backend services can be -
1. Authentication service.
2. Uploading service
3. Post creation service
4. Post listing service

Architecture diagram

![[namastedev.com_learn_namaste-frontend-system-design_hld-photo-sharing-app-instagram 1 1.png]]


### 3. Sometimes component architecture can also be asked in interviews

![[namastedev.com_learn_namaste-frontend-system-design_hld-photo-sharing-app-instagram 2 1.png]]

Dont waste much time in this , usually not asked in HLD system design interviews.

### 4. Data model

![[namastedev.com_learn_namaste-frontend-system-design_hld-photo-sharing-app-instagram 3 1.png]]

### 5. Decide APIs

Example the feedlist api - 

![[namastedev.com_learn_namaste-frontend-system-design_hld-photo-sharing-app-instagram 4.png]]

CreatePost API

![[namastedev.com_learn_namaste-frontend-system-design_hld-photo-sharing-app-instagram 1 2.png]]

#### We can have CDN as well to serve certain data

![[namastedev.com_learn_namaste-frontend-system-design_hld-photo-sharing-app-instagram 5.png]]


## 6. Optimization

1. Asset optimization
2. Feed Optimization

Assets - CSS, JS, images, videos

#### 1.1 Images

- Image format (WebP) - Superior image compression, one of the best format
- srcset
- userAgent - Which browser, OS, CPU related info and some other info. Using that we can decide image quality, etc. 
- dpr (device pixel ratio)
- Device connectivity / INternet connectivity
- Prefetch images

#### 1.2 Videos
- Streaming, image placeholders, quality, captions.
![[namastedev.com_learn_namaste-frontend-system-design_hld-photo-sharing-app-instagram 2 2.png]]

### 7. Implementation

Sometimes in some interviews, the interviewer might ask how we will implement this. How feasible it is and implementation details.

For example consider these 2 capabilities -
- Image editing
- Upload file


#### Image editing 
When you crop or edit images on an Instagram-like platform, the process involves two distinct stages: the **client-side manipulation** (UI/UX) and the **server-side persistence** (the API call).

##### 1. The Core APIs Involved

In a modern full-stack environment (like the one you might use with React and Node.js), these are the standard "APIs" or libraries used:

- **Client-Side (The "Editor"):** Instagram uses custom native libraries, but for web-based versions, it relies on the **Canvas API**. This allows the browser to redraw the image based on coordinates.
- **Android (Kotlin/Java):** Uses **OpenGL ES** or the newer **Vulkan API**. These allow the app to manipulate image textures directly on the graphics chip.

Using  these libraries on mobile phones helps using GPU for faster and efficient processing and also battery efficiency.

- **Storage API:** Images aren't usually stored directly in a database like MongoDB. Instead, they are sent to a **Cloud Storage API** such as **Amazon S3**, **Google Cloud Storage**, or **Cloudinary**.

- **The Backend API:** This is your custom endpoint (e.g., `/api/posts/create`) that handles the metadata and the link to the image.

---
##### 2. The Data Flow

Before the POST call happens, the app calculates the **Crop Logic**. It determines the $(x, y)$ coordinates and the height/width of the selection.

1. **Transformation:** The app creates a "blob" or a "base64" version of the edited image.
2. **Upload:** The file is sent to a storage bucket.
3. **Database Entry:** The final POST call sends the resulting URL to your server.

---
##### 3. How the POST Call Looks

When you hit "Share," the browser sends a `multipart/form-data` request. This is necessary because you are sending both text (caption, location) and a binary file (the image).


### Filtering logic 

### 1. In the Editor (The "Preview" Phase)

You are exactly right—on the web, filtering is often done using **CSS Filters**. When you click "Clarendon" or "Sepia," the app doesn't actually change the pixels of the file yet. It just applies a style to the HTML `<img>` or `<canvas>` tag.

- **How it looks in code:** `filter: brightness(1.2) contrast(1.1) sepia(0.3);`
    
- **The Benefit:** This is "instant." Since the browser is just changing how the image is _rendered_ on your screen, there is zero lag. It’s entirely non-destructive.

### Summary for System Design

- **Previewing:** Use **CSS** (Web) or **GPU Overlays** (Mobile). This is fast and saves battery because you aren't creating new files constantly while the user "tries on" different filters.
    
- **Persisting:** Use **Canvas.draw()** or **OpenGL/Vulkan** to render a final version. The "Post" call should ideally send a flattened, processed image so that the backend doesn't have to do heavy image processing work.

## Uploading image 
| **Feature**        | **Base64 Encoding**                                  | **Multipart HTTP POST**                          | **File Chunking**                                  | **Presigned URLs**                                       |
| ------------------ | ---------------------------------------------------- | ------------------------------------------------ | -------------------------------------------------- | -------------------------------------------------------- |
| **Data Format**    | Long Text String (JSON)                              | Raw Binary Data                                  | Sliced Binary Chunks                               | Direct-to-Cloud Binary                                   |
| **Payload Size**   | **+33% Overhead** (Heavy)                            | Original Size (Efficient)                        | Original Size                                      | Original Size                                            |
| **Best Use Case**  | Tiny icons, profile thumbnails, or quick prototypes. | Standard single-image uploads (Instagram posts). | Large files (4K Video) or flaky mobile networks.   | High-scale apps where the server shouldn't handle files. |
| **Reliability**    | Low (can crash browser if string is too long).       | Medium (if connection drops, you restart).       | **High** (Resumable; only re-upload failed parts). | **High** (Offloads work to professional cloud storage).  |
| **Server Impact**  | **High** (CPU/RAM used to decode string).            | **Medium** (Server must parse and relay data).   | **Medium** (Server must reassemble the chunks).    | **Lowest** (Server only generates a tiny text URL).      |
| **Implementation** | Very Easy                                            | Standard (using Multer/Busboy)                   | Complex (requires state tracking of chunks).       | Moderate (requires Cloud IAM setup).                     |
![[namastedev.com_learn_namaste-frontend-system-design_hld-photo-sharing-app-instagram.png]]

