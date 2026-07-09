
Mainly focus is on real time updates.

### Functional and non-functional requirements

This is not limited to cricket scores, it can be used in various other fields where we want real time updates.

![[namastedev.com_learn_namaste-frontend-system-design_hld-live-commentary-cricinfo-crickbuzz 2.png]]

## Architecture

#### 1. Real time updates using web sockets

![[namastedev.com_learn_namaste-frontend-system-design_hld-live-commentary-cricinfo-crickbuzz 1.png]]

Websockets can be used but it comes with a cost, as having millions of websocket connections open can put a lot of stress on the servers and resources.

Other alternatives used by crickbuzz and cricinfo tend to use a mixture of polling as well as websockets. Polling is widely used for cricket scores as we do not need exact real time updates, we can wait for 3-5 seconds.

Websockets are definitely good, but we need to see our scale and then decide if we should use it.

#### 2. Notifications

![[namastedev.com_learn_namaste-frontend-system-design_hld-live-commentary-cricinfo-crickbuzz 2.png]]


## System architecture

![[namastedev.com_learn_namaste-frontend-system-design_hld-live-commentary-cricinfo-crickbuzz 3.png]]

