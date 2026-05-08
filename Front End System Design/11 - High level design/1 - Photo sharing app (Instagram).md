
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