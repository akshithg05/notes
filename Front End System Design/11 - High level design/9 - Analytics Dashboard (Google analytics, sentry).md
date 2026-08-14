
### 1. Functional and Non Functional requirements 

In this module we wont be discussing these, we will go even more higher level and decide all the requirements.

### 1. Requirements

![[Front End System Design/images/namastedev.com_learn_namaste-frontend-system-design_hld-analytics-dashboard-google-analytics 1.png]]

### 2. Working

When a user acts on a website, the site sends an **event** through the **Google Tag** to the **Google Analytics** dashboard, which ==records and shows the data==.

How the Process Works

- **User Action:** A visitor clicks a button, plays a video, or buys an item on your web page.
- **Google Tag:** The tag (code on your site) catches this action and packages it into an event with details.
- **Google Analytics:** The data goes to your property, processes in the backend, and shows up in your reports and dashboards.

![[Front End System Design/images/namastedev.com_learn_namaste-frontend-system-design_hld-analytics-dashboard-google-analytics 1.png]]

### 3. Implementation

## 3.1. Screen recording - How MS Clarity will record the screen as a user performs operations on a screen.

Session recording tools (like Microsoft Clarity or Hotjar) do not record your physical screen. They do not capture video. Instead, they act like a **digital blueprint reader** inside the webpage code.
How It Works

- **Code Injection:** The website loads a small JavaScript script when you visit.
- **DOM Capturing:** The script takes a snapshot of the webpage's HTML structure (called the Document Object Model, or DOM). 
- **Event Logging:** As you move, the script logs your actions as text data:
    - _“Mouse moved to coordinates X:120, Y:350”_
    - _“User clicked on button ID 'play-video'”_
    - _“Page scrolled down 400 pixels”_
- **The Replay:** The tool sends this text log back to its server. The dashboard then plays back your actions by overlaying your recorded mouse movements and clicks onto the saved blueprint of the website.

You are watching a **reconstruction** of your session, not a video of your monitor.


## 3. 2.  JS Errors - We can track JS errors and log it onto our dashboards. This can be done by using custom try-catch blocks. We can also use window.onerror 

#### 3.2.A Navigation timing API

![[namastedev.com_learn_namaste-frontend-system-design_hld-analytics-dashboard-google-analytics 1 1.png]]

#### 3.2.B Performance API

![[namastedev.com_learn_namaste-frontend-system-design_hld-analytics-dashboard-google-analytics 2.png]]

### 3.3. Tracking all User activity


## 4. Vizualization

![[namastedev.com_learn_namaste-frontend-system-design_hld-analytics-dashboard-google-analytics 3.png]]

