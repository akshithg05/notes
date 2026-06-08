This is one of the most asked interview question, we need to build around this. Multiple angles and implementation details are there for this problem statement.

Problem statement - Build a news feed. -> This should be the focus in this problem, not other things.

1. Feed - Collection of posts
2. If we post a post, it will become part of the feed.
3. Filter based on trending , tags , etc.

As usual 2 parts -

1. Functional requirement 
2. Non functional requirements

![[namastedev.com_learn_namaste-frontend-system-design_hld-News-media-feed-facebook-twitter 2.png]]


1. If you are junior dev you might be asked to do the component architecture.

You can just explain the component structure easily.

## 2. Architecture 

Some interesting things to discuss - Liking and comment strategy , updates and UI representation
![[namastedev.com_learn_namaste-frontend-system-design_hld-News-media-feed-facebook-twitter 1 1.png]]

## Data Model (always think about normalization)

Data needs to be modelled and stored in a normalized fashion. Do not repeat yourself (DRY).
Avoid nesting, maintain normalization.

![[namastedev.com_learn_namaste-frontend-system-design_hld-News-media-feed-facebook-twitter 2.png]]



## Implementation details 

#### 1.  Rendering approach

SSR, CSR, SSG, React component etc. For news feed kind of application, its dynamic data.
Initial set of posts can be server side rendered, then rest all are client side rendered. So therefore SSR + CSR rendering.

#### 2. Pagination (Infinite scroll)

Can't load all data at once, so maybe load around 20 posts at a time. Once we reach the end of the feed, load 10 or 15 more posts. 
 2 ways - Offset based, cursor based pagination.


Technical Notes: Feed Pagination & Real-Time Refreshing

1. The Core Problem with Offset Pagination (`LIMIT/OFFSET`)

- **How it fails**: Real-time apps (Instagram, X, News Feeds) constantly receive new data.
- **The bug**: If a user is on Page 1 and new posts are added, existing posts get pushed down. When the user requests Page 2, they see the same items they just saw on Page 1, resulting in **annoying duplicate records**.
- **Performance issue**: Deep pages get progressively slower (O(N)) because the database must scan through all skipped rows.

2. The Solution: Cursor-Based Pagination

- **How it works**: Instead of skipping a numerical offset, the API anchors queries to a unique, sequential pointer (a **cursor**) from the last item seen.
- **The database behavior**: Uses strict filtering (`WHERE id < :cursor`) combined with database indexes. This runs at a constant speed (O(1)) regardless of feed depth.
- **The benefit**: Data remains mathematically locked in place. New upstream items do not shift or duplicate the historical data lower down the feed.

3. How Real-Time Feed Refreshing Works

To handle updates, the client application tracks two distinct cursor pointers simultaneously:

1. **`next_cursor` (Bottom Pointer)**: Tracks the _oldest_ post on screen. Used for infinite scrolling downwards (`WHERE id < :next_cursor`).
2. **`since_id` / `top_cursor` (Top Pointer)**: Tracks the _newest_ post at the very top of the screen. Used for refreshing upwards.

3. Step-by-Step Refresh Workflow

- **Background Check**: Every 30–60 seconds, the client sends a background ping using `WHERE id > :since_id` to check for newer items.
- **The UI Trigger**: If new items exist, the UI displays a "New Posts" pill or awaits a manual pull-to-refresh action.
- **Prepend Data**: When triggered, the client fetches the new records, **prepends** them to the top of the feed array, and updates the `since_id` to the latest post ID.

---

![[namastedev.com_learn_namaste-frontend-system-design_hld-News-media-feed-facebook-twitter 3.png]]
![[namastedev.com_learn_namaste-frontend-system-design_hld-News-media-feed-facebook-twitter 1 1.png]]

Preserving scroll positions

#### 3.Tagging functionality-

For tagging people and using hashtags we cant use text/area
We can use div + content editable
We can use WYSYWIG editor , best option. - draft.js, slate.js

#### Optimistic UI updates

The Step-by-Step Flow

1. **Instant Feedback:** You hit "Post" or "Like". The frontend instantly updates your local state and UI (e.g., your comment appears immediately, the heart button turns red).
2. **Silent Syncing:** In the background, the app fires an asynchronous API request to the server to save the data.
3. **Success:** The server processes the request and confirms it. The app does nothing (or silently swaps the temporary local ID for the permanent database ID).
4. **Failure (Rollback):** If the network fails or the server rejects the action, the app quietly removes the post/like from your screen and displays an error message (e.g., "Failed to post. Try again").

Common Use Cases

- **Likes & Reactions:** Tapping a heart fills the icon instantly; the app updates the like count by +1 without waiting for the database response.
- **Comments:** Your new comment is appended to the thread locally.
- **Uploading Posts:** The app shows a greyed-out or blurred "posting..." placeholder image while the file uploads to cloud storage in the background.

Why Frontends Use It

- **Perceived Performance:** It eliminates the delay caused by network latency, making the app feel snappy and instant.
- **Resilience:** Users can continue scrolling and interacting without waiting for one action to finish before starting another.
- **Higher Engagement:** Apps that feel instantaneous psychologically encourage users to interact more freely. [[1](https://blog.devgenius.io/supercharge-your-next-js-f3fa298eaf10), [2](https://www.youtube.com/watch?v=cypK50wBCZs), [3](https://namastedev.com/blog/implementing-optimistic-ui-updates-in-react-applications/)]

The Technical Challenges

- **Handling Errors:** Developers must write complex rollback logic to undo the UI change if the network request fails.
- **State Reconciliation:** When multiple actions happen rapidly, the frontend must ensure the local cache correctly syncs with the true server state. [[1](https://www.freecodecamp.org/news/how-to-use-the-optimistic-ui-pattern-with-the-useoptimistic-hook-in-react/)]

![[namastedev.com_learn_namaste-frontend-system-design_hld-News-media-feed-facebook-twitter 4.png]]

![[namastedev.com_learn_namaste-frontend-system-design_hld-News-media-feed-facebook-twitter 1.png]]

