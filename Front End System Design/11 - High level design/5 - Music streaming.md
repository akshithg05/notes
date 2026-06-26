
![[namastedev.com_learn_namaste-frontend-system-design_hld-music-streaming-spotify.png]]

Main focus in the functional requirement side is -
1. Music player
2. Download music

Non-functional requirements side -
1. Offline support
2. Custom Control

Tech stack and tech choices (In senior engineer roles)-
1. Frontend - React (web), iOS (Swift), Android (Kotlin, Flutter, React Native).
2. Backend - Node/Express, Java/Springboot, Python, Go.
3. Database - PostgreSQL , MongoDB
4. Storage - AWS (s3)
5. CDN - AWS (Cloudfront), Cloudfare
6. Auth - OAuth 2.0, JWT
7. Hosting - AWS, Azure, Google Cloud Platform (GCP).

## Architecture - (High Level)


Anytime the view layer (UI) makes a request to the controller, controller sends request to the service. Services says I need to get a song (binary files) -
1. First the browser cache is checked (service worker)
2. Service worker checks if data is present, if the user is online/ offline and then returns the data either from the cache or fetch it from the backend and serves the view layer.
![[namastedev.com_learn_namaste-frontend-system-design_hld-music-streaming-spotify 1.png]]


### Offline support

1. For mobile applications offline support is easier to implement as the app is on the local storage of the phone and music also can just be stored locally.

#### 2. Offline support for browsers

Music player implementation
