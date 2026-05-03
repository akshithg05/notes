
1. Do not blindly read from book / notes / videos. We need to understand the expectation of the interviewer and understand the question well.

2. Feel free to ask the interviewer what the application does, what are the features and what are the expectations, if you haven't worked on the application before.

### Problem statement for instagram

#### Categorize into 2 -

1.Functional requirement -

2.Non functional requirement.

(No coding involved)

![[namastedev.com_learn_namaste-frontend-system-design_hld-photo-sharing-app-instagram.png]]


### Architecture design

Views - What you see. Eg - Lists, creation
Controller - Consists of the main business logic of our application. How our views are powered. Eg- Filtering, Editing, Upload. (All these can be used for posts, reels and stories, common logic).

Then we can have specific controllers like - PostListing, ReelsListing, StoryListing, PostCreation.

**Note**: - Sometimes we are from different backgrounds (React, Angular, Vue). Try to be generic, do not be specific like useEffect or useState. Try to use terms like controllers and Views instead.

![[namastedev.com_learn_namaste-frontend-system-design_hld-photo-sharing-app-instagram 2.png]]

This is enough for anyone who is a mid-range software engineer.

Try to also talk about microservices. How client interacts with upstream layers and projects.





