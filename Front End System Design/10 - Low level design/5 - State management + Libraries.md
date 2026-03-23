Every UI application has 2 layers - 

1. UI Layer - Presentational elements and anything that one can see on a web page.
2. Data Layer - UI Layer is controlled by the data layer. The value of the dynamic data in the UI elements are coming from the data layer.

UI - HTML
Data -JS , data, variables ,logic.

These both work in sync. UI layer is powered by the data layer.

![[namastedev.com_learn_namaste-frontend-system-design_lld-state-management (1).png]]

90% of bugs we get are due to data layer errors.

### Why do we need state ?

Because of dynamic behavior of data within UI elements.

1. Local state (component state).
2. Props drilling (Passing data b/w components).
3. Context API in React.
4. State management libraries.

#### 1. Example - 
For rendering a card with image we need - image url, title and some description.

![[namastedev.com_learn_namaste-frontend-system-design_lld-state-management (1) 1.png]]

For managing this card data we need local state.

**Local state** - used for managing any dynamic data in a component.

Code of the card remains same, the data changes.

2. **Example-** 
Suppose we have a big application with many components. And inside these as well we have many smaller components. State of our application depends on how components are interacting with each other.

Local state - scope is component level.
Local state can also be accessed by the children of a component if it is passed as props. This is the single way data flow concept in react.

Data flow is unidirectional - Parent --> Child component.

3. **Example -** 
if we have a list of books to be rendered, the list is in the parent and the data is passed into the children elements as props. Parents pass props to children. Children cannot send data to parent.

### Props drilling
This concept of passing data from paren to child to child to child just to pass data but not using that data in the intermediate components, is called props drilling.

**Prop drilling** in React is the process of passing data (props) from a parent component down through multiple layers of intermediate components in the component tree to a deeply nested child component that actually needs the data. The intermediate components do not use the data themselves; they merely act as a conduit to pass it further down.

### Lifting the state up
If two siblings want to share the same data, this state definition should be moved to the parents and the parent can then pass the data to all the children components as props.

### React context API

The **React Context API** is a built-in feature that enables sharing data across components without manually passing props at every level of the component tree (a process known as "prop drilling"). It's especially useful for sharing "global" data like UI themes, authenticated user status, or language preferences
### State management libraries

1. Redux
2. Zustand

#### Why do we need state management libraries ?

In large scale applications the component hierarchy is huge. Data sharing through props can be done, but this will be messy, unmaintainable and unreadable.
It is difficult to make changes and manage state.

State management libraries create a central global state (store in Redux). It manages the state of the entire app. 

The same value can be read by multiple components anywhere in the application.

Redux works as a subscriber model. The components can subscribe to a state variable in the store and whenever the state changes , it will be rendered in the component. Multiple components can read and write data from this store. Changes are automatically reflected across.

Dont use state management libraries for very small projects. It is not required until and unless the application is large.

Read about redux in namaste react notes.

Summary - central store to track all data, component subscribed to store.
![[namastedev.com_learn_namaste-frontend-system-design_lld-state-management (1) 2.png]]



