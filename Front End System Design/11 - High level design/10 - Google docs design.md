Mainly building real time collaboration and real time editing. This is beyond real time chatting and it is about real time collaboration.

In google docs if one user is making the changes the other user must see it on his browser window.

Same piece of the document is being collaborated by multiple people.

### 1. Functional requirements

1. Multiple participants
2. Updates by peer should be reflected in real time.
3. Same version should be visible to all participants.
4. Conflict resolution

### 2. Non functional requirements

1. Real time 
2. Collaboration (100 concurrent users)
3. Offline support 
4. Performance (max 500ms)
5. No geo barrier

### 3. Implementation details

1. Real time collaboration 
2. WYSIWIG editor / Text editor.

These collaborations should happen across the world. There should not be any geographical barriers.

### 4. Data

 Request payload 
- Send entire data (not usually preferred method)
- Send delta (More preferred method) 

Communication Model
- Client server model
- Peer to peer model

![[namastedev.com_learn_namaste-frontend-system-design_hld-google-docs.png]]

In google docs its better we have a client server model as every client should be on the same version and sending delta works better. This is because in a system like Google docs, we cannot have any kind of data losses. Every bite and bit is important.

### 5. Concurrency 

#### 5.1 Control models

- Update changes locally
- Merge updates from peers.

#### Types

1. Pessimistic Approach - Any change we make/ update we make, in order to reflect these changes, send it to the server and then the server pulls the changes from the peers and then sends the final copy to the clients 

2. Optimistic Approach - Make changes locally and at the same time the changes are being sent to the server also and we keep pulling changes from server to merge the changes of the peers.

#### 5.2 Control Mechanisms

 If in case, people have to edit and there are issues/ conflicts and different versions, which version is the final one ?, all these needs to be taken care of.

1. Last write wins model - Whoever uploads last
2. Floor Control Model
	- Token based
	- Chair controller
3. Lock model - whoever starts typing , that version is locked. This has its own challenges.
4. Transaction based model 
5.  Version detection model - Everyone has their own version and making updates. If u are on latest version server takes your delts and pushes it to all other peers. If you are not on the latest version then you take the latest version tehn apply your delts.

We will use the Optimistic approach and the version detection model.




