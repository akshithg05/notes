This is about building a whiteboard. Example - miro, draw.io, paint, ms whiteboard.
Various colours, shapes, text etc.

### 1. Functional and Non functional requirements

![[Front End System Design/images/namastedev.com_learn_namaste-frontend-system-design_hld-diagram-tools-excalidraw 2.png]]

### 2. Architecture (Client side)

![[namastedev.com_learn_namaste-frontend-system-design_hld-diagram-tools-excalidraw 1 1.png]]



### Design considerations

How do we get the board -
Canvas API / SVG - Both can be used to create white boards.

![[Front End System Design/images/namastedev.com_learn_namaste-frontend-system-design_hld-diagram-tools-excalidraw 2.png]]

#### SVG 


![[namastedev.com_learn_namaste-frontend-system-design_hld-diagram-tools-excalidraw 1 1.png]]

SVG is vector based and not picture based so we will not see pixels and distortion when zoomed in.

![[namastedev.com_learn_namaste-frontend-system-design_hld-diagram-tools-excalidraw 2 1.png]]


Canvas api is faster, SVG is heavy and slow as heavy dom operations are performed.

##### Generally it is advised to use a combination of canvas and SVG. This is because SVG is more interactive and easy to maintain. Canvas is more scalable and easy to to go to large scale. This is not generally done but good practice.

## Interface

Storing these shapes/ board related information - 

![[namastedev.com_learn_namaste-frontend-system-design_hld-diagram-tools-excalidraw 4.png]]

### Database

If we want sync between various tabs, we need localStorage over Index DB. Of course Index DB can be optimized and programmed to sync but localStorage has this capability out of the box.

IndexDB is more structured and has a steeper learning curve. To store on localStorage we need to stringify to store and destringify to access it everytime.



