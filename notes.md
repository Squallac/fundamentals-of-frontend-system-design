# Box Model

Box properties: Block size y block type

# Browser formatting context

Cuando un elemento nuevo es creado, entra al formatting context actual, si ese elemento lleva estilos, se crea un nuevo formatting context isolado. Por ejemplo los spans crean inline formatting context de manera implicita.

3 key ideas

1. Isolation: Elements within the context are shielded from external rules,
2. Scalability: New rule sets can be introduced by creating a new context,
3. Predictability: A strict set of rules allows for consistent element positioning

The block formatting context is set by default when an HTML page is initiated

# Dom Templating Exercise

The <template> tag stores HTML in a lightweight object in memory, which is not queryable by DOM API, not rendered in the final render tree, and allows for creating reusable HTML components

Document fragments exist in memory and do not trigger reflow, allowing for efficient modifications without causing performance overhead in the DOM tree

la solucion esta en la branch 1-dom-end

# Observer API

![Oberserver API Diagram](observerAPI.png)

- What are the three main types of the Observer API?
  Intersection Observer, Mutation Observer, and Resize Observer

- What is an Intersection Observer primarily used for?
  Virtualization pattern, lazy component rendering, analytics tracking of website visibility, and creating dynamic UI elements

- What properties does an Intersection Observer configuration object typically have?
  Root (container being tracked against), threshold (ratio of intersection), and callback function

- How much faster are Intersection Observers compared to vanilla JavaScript tracking approaches?
  On average, 50 times faster, it has an observer that checks all the elements

- What are the two cases when an Intersection Observer callback is triggered?
  When the target element starts intersecting and when the intersection stops

- What property helps determine if an element is currently intersecting?
  isIntersecting

- What are the two parameters accepted by the Intersection Observer constructor?
  Callback function and config object

### Infinite scroll with intersection observer

coding branch `2-intersection-observer-begin` y solucion `2-intersection-observer-end`

- What method is used to minimize DOM mutations when adding new elements?
  Using a document fragment to accumulate DOM updates before appending them to the list in a single operation

- What configuration parameter is set for the Intersection Observer?
  The threshold is set to 0.2, which means the callback will trigger when 20% of the observed element is visible

- How is the page number tracked when fetching new data?
  A variable is initialized to 0 and incremented by 1 each time new data is fetched

- What steps are involved in rendering new cards?
  Fetch new data using MockDB
  Create a document fragment
  Create card elements for each data item
  Append card elements to the fragment
  Append the entire fragment to the list container

## Mutation observer

- What is the primary purpose of the Mutation Observer in JavaScript?
  The Mutation Observer allows tracking changes within the DOM subtree, such as detecting modifications to child elements, attributes, or text content at a native level, which is particularly useful for applications like rich text editors.

- What are the main configuration options for a Mutation Observer?
  The main configuration options are: childList (track direct child changes), attributes (track attribute modifications), characterData (track text content changes), and subtree (track changes across the entire subtree). Best practice is to configure these options carefully to avoid excessive callback invocations.

- What properties does a Mutation Record provide?
  A Mutation Record provides properties including: type (mutation type like attribute change or element addition), target node (which triggered the mutation), added/removed nodes array, and old character data value for tracking changes in the DOM.

- What advantage does a native Mutation Observer have over previous JavaScript-level implementations?
  A native Mutation Observer is implemented at the browser level, which makes it much faster and more memory-efficient compared to previous JavaScript-level polyfills that would create proxy objects to track mutations.

- What happens if both 'childList' and 'subtree' options are set to true in a Mutation Observer?
  When both 'childList' and 'subtree' are set to true, the 'childList' option takes precedence, which means the subtree option will not work, and only direct child changes will be observed.

### Mutation observer Exercise

branch: ` 3-mutation-observer-start`

- What attribute makes an HTML element editable by the user?
  content-editable="true"

- What are the key steps in creating a Mutation Observer?
  Create a mutation observer with a callback function, 2. Filter for specific mutation types, 3. Check target element and text content, 4. Replace element if conditions are met, 5. Observe the target element with configuration settings

- What mutation type is used to track typing or text changes in a Mutation Observer?
  characterData

- What configuration property allows deep checking of DOM changes in a Mutation Observer?
  subtree: true

- What method is used to replace an existing DOM element with a new element?
  replaceWith() method

## Resize Observer

- What are the two main methods for handling changes when resizing a web page?
  CSS media queries and the resize event

- Why is the resize event considered slow?
  Because it relies on standard DOM events, requires traversing the entire DOM tree, and can be fired up to 5,000 times during a small resize

- What is the primary advantage of ResizeObserver over the resize event?
  ResizeObserver is approximately 10 times faster, supports callbacks, and can track multiple element resizes simultaneously

- What two box types can be used with ResizeObserver?
  Content box (tracks inner rectangle size) and border box (includes border and padding in resize calculations)

- Why does ResizeObserver return an array of boxes instead of a single box?
  The specification anticipates future HTML elements with multi-column layouts, allowing potential tracking of multiple boxes within a single element

### Resize Observer Exercise

branch `4-resize-observer-start`

- What is the primary purpose of using the ResizeObserver API?
  To track changes in element sizes and trigger callbacks when those sizes change, such as updating styles or layouts in a performant way, particularly useful for applications with multiple windows or dynamic content

- What browser support does the Observer API currently have?
  The Observer API has approximately 98% client support, with the option to use a polyfill for the remaining 2% of clients

- How do inline size and block size values change with different text rendering directions?
  The inline and block size values adapt based on text rendering settings like LTR (left-to-right), RTL (right-to-left), or vertical text, potentially swapping width and height tracking based on the rendering perspective

- What is a recommended performance optimization strategy for MutationObserver?
  Provide specific configuration to track only necessary changes, filter out unnecessary attribute or node changes, and consider tracking mutations dynamically on specific elements rather than the entire document tree

# Virtualization

branch `5-1-virtualisation-skeleton-start`

## Virtualization technique

- What is virtualization in the context of web development?
  A UI optimization technique that maintains data in virtual memory while rendering only a limited subset of the data, minimizing DOM elements, reducing mutations, and decreasing CPU and memory usage

- What are the two key observers in the virtualization technique?
  The top observer, which handles scrolling up, and the bottom observer, which handles scrolling down, with a viewport that triggers loading of new data when touching these observers

- What is the primary goal of element recycling in virtualization?
  To reuse existing DOM elements when rendering new content, instead of creating new elements each time, which helps reduce memory usage and improve performance

- What utility function is used to move elements around in the virtual list?
  The translateY function, which returns a CSS transformation to move elements vertically

- What does the y() function do in the virtual list implementation?
  It sets or retrieves the 'data-y' attribute on an HTML element, converting the value to a number if a value is provided, or returning null if no value exists

## Coding from scratch

- What are the main components of the HTML structure being created?
  The structure includes a container, top-observer element, virtual-list, and bottom-observer element

- What configuration parameter is set for the intersection observer?
  The threshold is set to 20%

- What two cases are being handled in the intersection observer callback?
  Checking the top-observer and bottom-observer elements, and determining if they are intersecting

- What method is called when the bottom-observer is intersected?
  handleBottomObserver method

- When comparing getAttribute and dataset API for accessing data attributes, what is the key consideration?
  It is mostly a matter of personal preference, with no clear technical advantage to either approach

## Loading new data

- What is the purpose of the 'getTemplate' function in a virtual list?
  The getTemplate function accepts a single piece of data and returns a newly created HTML element, allowing the virtual list to work with generic HTML templates defined by the user

- What is the difference between 'getTemplate' and 'updateTemplate' functions?
  getTemplate creates a new HTML element for each data item, while updateTemplate modifies an existing element with new data instead of creating a completely new element

- What are the two pointers used in managing the virtual list's state?
  The start pointer and end pointer, which are used to track the current rendering window and incrementally load new pages of data

- What is the concept of virtualization in this context?
  Virtualization is a sliding window technique where only a specific subset of data is rendered at a time, with the ability to dynamically load more data as the user scrolls

- What is the purpose of the page size property in the virtual list?
  Specifies the number of elements to render per API call

## Creating virtualization pool

- What is the purpose of setting a limit for rendering elements in virtual scrolling?
  To maintain a fixed number of elements in memory, preventing unlimited rendering and improving performance by keeping only two pages worth of elements at a time

- What does the slicing operation do when managing the virtual memory array in virtual scrolling?
  It splits the pool of elements into two halves: a 'recycle' half and an 'unchanged' half, allowing for efficient element reuse and memory management when scrolling

- What are the two primary steps when updating elements during virtual scrolling?
  First, swap the halves of the element pool in memory, and second, update the data content of the recyclable elements with newly fetched data

- How is the limit for virtual scrolling typically calculated?
  The limit is set as double the page size, which ensures that two complete pages of elements are always maintained in memory

- What is the primary goal of the update data function in virtual scrolling?
  To update the text content of recyclable elements with newly fetched data without physically moving the elements in the viewport

## Recycling elements

- How is the position of a card calculated during virtualization?
  The position is calculated by taking the previous item's y position, adding its height, summing the margins, and then applying CSS transformation to position the card accordingly

- What is the strategy for handling the first element's y position during virtualization?
  The first element's y position is initialized to 0, allowing subsequent elements to calculate their positions based on previous elements

- Why are elements moved to an absolute positioning context during virtualization?
  To prevent the browser from rendering elements in normal flow and allow precise pixel-level positioning using CSS transformations

- How do observers track the position of virtualized elements?
  Observers are positioned based on the y position of the first and last elements in the pool, with top observer placed before the first element and bottom observer placed after the last element

- What technique is used to efficiently move elements during virtualization?
  GPU-accelerated CSS transformations using translateY, which moves elements to a separate stacking context without modifying the DOM

## Virtualization pool QA

- When is virtualization typically recommended?
  Virtualization is recommended for mobile apps where memory usage needs to be minimized, such as social network apps or rendering tables with thousands of elements. It helps prevent overusing memory by rendering only a limited number of elements.

- What is the key difference between virtualization and lazy loading?
  In virtualization, a constant number of nodes is maintained (e.g., limit of 20 elements), while lazy loading allows appending new elements to the screen without recycling previously rendered elements.

- What happens when position is set to absolute in terms of element positioning?
  When position is set to absolute, all elements' positions are reset to the top-left most quarter. This allows for easier positioning using transformations and relative container references.

- How does setting position to absolute affect the rendering pipeline?
  When adjusting the position of absolute elements, it triggers a reflow. However, using transform can optimize the pipeline, triggering only the GPU pipeline without impacting the rendering thread, making it faster.

## Handle top virtualization

- What is the primary strategy for implementing top virtualization in this context?
  Reverse the direction of rendering by moving elements from the top, exchanging array halves, and setting elements' positions relative to existing rendered items, starting from the end of the page size and moving backwards

- How is the new y-position calculated for an element during top virtualization?
  The new y-position is calculated by taking the next element's y-position, subtracting the margin twice, and then subtracting the current element's height

- What condition prevents top intersection observation when scrolling to the very top of the list?
  The top intersection observer should not be triggered when the start pointer is zero, which indicates no more elements can be virtualized from the top

- How is the scroll bar height maintained during bottom scrolling?
  By setting the container's height style to match the scrollHeight property, which ensures the scroll bar maintains its size when new elements are dynamically loaded

- What is the key difference between bottom and top virtualization approaches?
  In bottom virtualization, elements are added from the bottom, while in top virtualization, elements are added from the top by moving backwards through the array and calculating positions relative to existing rendered elements


# Application State & Network Connectivity

## Application State Design
What are the two key properties of UI state data?
Data type/class and data properties. Data types can include app configuration, UI element state, or server data, while data properties include access level, read/write frequency, and size.

What are the three general principles for designing application state?
Minimize data access cost (aim for constant time access), 2. Optimize search operations, 3. Optimize memory usage by reducing unnecessary object storage

What is data normalization and what are its primary goals?
Data normalization is a concept from database design used to optimize how data is stored in UI applications. Its primary goals are: (1) provide optimized access performance, (2) create a unified, optimized structure for storing data, and (3) increase code readability and maintainability. It operates using normal forms (typically 1st, 2nd, and 3rd normal forms in UI apps) to systematically structure data.


What are the three normal forms typically used in UI applications, and what does each form require?
1st Normal Form: Every field should be atomic (reduce object nesting), flatten nested objects, and establish a primary key. 
2nd Normal Form: All fields should depend on the entity's primary key. Fields that depend on other non-primary keys should be decoupled into separate tables/objects. 
3rd Normal Form: Non-primary keys should depend only on the primary key (enforces stricter dependency than 2nd Normal Form - e.g., if department depends on job_id rather than the entity's primary key, move it to a separate table).

What are the three types of storage APIs and their key characteristics?
1. Session Storage: Stores small, non-persistent data for a single session only (wiped when the website is closed). Supports only string type and is synchronous (blocks UI thread). 
2. Local Storage: Stores small data with persistence. Supports only string type and is synchronous (blocks UI thread), so not ideal for frequently read/written data. 
3. IndexedDB: Supports large storage (around 3 GB), multiple data types, indexing, and is asynchronous (non-blocking), making it suitable for frequently accessed data.

## Network Connectivity

What are the two main network protocols discussed, and what is a key difference between them?
UDP and TCP. UDP does not guarantee package delivery and can lose data, while TCP ensures full data delivery through a 3-way handshake and guarantees data integrity.

What are the energy consumption implications of long polling on mobile devices?
Long polling forces mobile devices to use a duplex network mode, which is not energy efficient. It can potentially drain a 2000mAh battery in almost four hours by maintaining an open socket.

What are the key protocols built on top of TCP and UDP?
On TCP: HTTP 1.1, HTTP 2, Server-Sent Events (SSE), and WebSockets (which use HTTP 1 for initial handshake then upgrade to pure TCP);
On UDP: QUIC (developed by Google), WebRTC, and HTTP 3 (which is based on QUIC)

What are the network inefficiencies of using long polling?
Long polling requires establishing a new TCP socket for each request via a 3-way handshake, which is slow. Each request sends metadata headers with the request—in HTTP/1, headers are uncompressed and can be up to 50KB of overhead data. HTTP/2 compresses headers but still requires the 3-way handshake. On mobile devices, latency increases significantly when switching between network towers during travel, requiring connection reestablishment. Additionally, because HTTP requests are stateless, reconnection infrastructure must be implemented on the server side.


In which scenarios is long polling most appropriate?
Long polling is best suited for desktop applications where network bandwidth, latency, and energy consumption are not critical concerns. It is easy and cheap to implement with minimal infrastructure requirements. However, it should be avoided for mobile applications because it drains battery by maintaining TCP sockets open (which forces the mobile antenna into less efficient duplex mode), is network inefficient due to repeated headers and 3-way handshakes, and can have high latency when switching between network towers.

## Server-sent events
What is the key communication characteristic of Server-Sent Events (SSE)?
Server-Sent Events use a unidirectional server-push technology where duplex communication is only used for the initial connection handshake, and the rest of the connection operates in receive-only mode with the server continuously pushing data to the client.

What is a key advantage of Server-Sent Events in terms of infrastructure scaling?
SSE allows easy horizontal scaling, where requests can be forwarded to different server instances without losing connection state, and you can always resume from the previous place

What is a limitation of Server-Sent Events in terms of data transmission?
Server-Sent Events can only push string data and do not support sending data from the client back to the server

How does HTTP2 multiplexing improve connection efficiency in Server-Sent Events?
HTTP2 multiplexing allows opening up to 200 requests within a single TCP socket, compared to traditional methods that require opening multiple TCP connections for different resources

In what scenarios are Server-Sent Events particularly beneficial?
SSE is beneficial for both desktop and mobile applications, provides performance comparable to WebSockets, and is especially useful for streaming large text data. It's particularly advantageous because reconnection is handled automatically at the protocol level, horizontal scaling is easier (can switch between server instances seamlessly), it's more battery-efficient for mobile devices, and it doesn't send unnecessary header overhead.
