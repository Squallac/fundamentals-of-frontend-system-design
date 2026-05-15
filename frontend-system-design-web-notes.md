
# Front-End System Design | Frontend Masters

### Introduction

**Introduction**

[00:00:15](https://frontendmasters.com/courses/frontend-system-design/introduction?t=15)
Here's a link to [the slides](https://static.frontendmasters.com/assets/courses/2024-07-23-frontend-system-design/frontend-system-design-slides.pdf)

[00:01:19](https://frontendmasters.com/courses/frontend-system-design/introduction?t=79)
Check out our [Introduction to Backend Architectures](https://frontendmasters.com/courses/backend-architectures/) course

### Core Fundamentals

**Box Model**

[00:00:08](https://frontendmasters.com/courses/frontend-system-design/box-model?t=8)
Here's a link to [the slides](https://static.frontendmasters.com/assets/courses/2024-07-23-frontend-system-design/frontend-system-design-slides.pdf)

[00:02:01](https://frontendmasters.com/courses/frontend-system-design/box-model?t=121)
Box properties: Block size y block type

[00:02:59](https://frontendmasters.com/courses/frontend-system-design/box-model?t=179)
See [Block Formatting Context](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_display/Block_formatting_context) on MDN

**Browser Formatting Context**

[00:00:12](https://frontendmasters.com/courses/frontend-system-design/browser-formatting-context?t=12)
Browser formatting context

[00:02:39](https://frontendmasters.com/courses/frontend-system-design/browser-formatting-context?t=159)
Note: the `section` should be after the `ul`

[00:03:40](https://frontendmasters.com/courses/frontend-system-design/browser-formatting-context?t=220)
Note: paragraph elements don't inherit display properties by default

**Browser Positioning**

[00:00:07](https://frontendmasters.com/courses/frontend-system-design/browser-positioning?t=7)
Note: The "right to left" and "left to right" labels should be switched

[00:04:43](https://frontendmasters.com/courses/frontend-system-design/browser-positioning?t=283)
Pos absolute

**Reflow**

[00:00:28](https://frontendmasters.com/courses/frontend-system-design/reflow?t=28)
El browser usa 2 arboles, DOM y CSSOM, se usan para crear render tree. Reflow ocurre cuando el JS trata de modificar el árbol o los estilos. Para optimizar CPU, usar GPU, ejemplo animación optimizada usando transform: translateY

[00:03:26](https://frontendmasters.com/courses/frontend-system-design/reflow?t=206)
Here's a link to [the CodePen](https://codepen.io/RayEuji/pen/JjyqQvw)

[00:04:10](https://frontendmasters.com/courses/frontend-system-design/reflow?t=250)
Click the label at the top to change the rendering mode

**Composition Layers**

[00:00:13](https://frontendmasters.com/courses/frontend-system-design/composition-layers?t=13)
New browsers use CPU and GPU in parallel to render the pageRender layer for element is constructed when element:- has explicit css properties : pos abs, rel, transfor- if its the root object of the page html- if its transparent- has a css filter- corresponds to canvas element that has a 3D webGL contextgraphic Layer is constructed when:- render layer has 3D or perspective transform CSS properties, - layer is used by video or canvas element- etc, graphic layer is very expensive to the browser so be careful https://csstriggers.com/ websites usually use 100s MB for rendering

[00:04:14](https://frontendmasters.com/courses/frontend-system-design/composition-layers?t=254)
Here's a link to [the demo](https://codepen.io/RayEuji/pen/qBwNbLm)

[00:04:24](https://frontendmasters.com/courses/frontend-system-design/composition-layers?t=264)
Debug Mode is only available for your own CodePens. Fork this example to access Debug Mode.

[00:04:33](https://frontendmasters.com/courses/frontend-system-design/composition-layers?t=273)
Layers can be found under the three dots > More Tools > Layers

[00:07:09](https://frontendmasters.com/courses/frontend-system-design/composition-layers?t=429)
The site is [CSS Triggers](https://csstriggers.com/)

### DOM API

**DOM & Querying**

[00:03:22](https://frontendmasters.com/courses/frontend-system-design/dom-querying?t=202)
checar el diagrama DOM API: Class Hierarchy. GetElementByid es el mas eficiente pero no hay abusar de las idsQuerySelector es poquito peor que getelementbyid pero no tiene live view

[00:03:30](https://frontendmasters.com/courses/frontend-system-design/dom-querying?t=210)
The code in the upper right box is `document.getElementById("content")`

[00:06:15](https://frontendmasters.com/courses/frontend-system-design/dom-querying?t=375)
The code in the upper right box should be `document.getElementsByTagName("p")`

[00:06:25](https://frontendmasters.com/courses/frontend-system-design/dom-querying?t=385)
The code in the upper right box is `document.querySelector("main.container")`

[00:09:52](https://frontendmasters.com/courses/frontend-system-design/dom-querying?t=592)
The code in the upper right box should be `document.getElementsByTagName("p")`

**DOM Performance Best Practices**

[00:01:29](https://frontendmasters.com/courses/frontend-system-design/dom-performance-best-practices?t=89)
perf best practices: simplify selector, use ids of core containers, pick the right start point

[00:04:13](https://frontendmasters.com/courses/frontend-system-design/dom-performance-best-practices?t=253)
Is better to use insertAdjacentElement or appendChild instead of innerHTML or insertAdjacentHTML, these have extreme impact

**DOM Templating Exercise**

[00:00:45](https://frontendmasters.com/courses/frontend-system-design/dom-templating-exercise?t=45)
Here's a link to [the repo](https://github.com/EvgeniiRay/fundamentals-of-frontend-system-design)

[00:02:22](https://frontendmasters.com/courses/frontend-system-design/dom-templating-exercise?t=142)
<template> guarda el html como un objeto en la memoria, no es queryable por el DOM API no es rendereado en el render tree

[00:06:03](https://frontendmasters.com/courses/frontend-system-design/dom-templating-exercise?t=363)
The solution can be found on the [1-dom-end branch](https://github.com/EvgeniiRay/fundamentals-of-frontend-system-design/blob/1-dom-end/1-dom/end/index.html)

[00:06:09](https://frontendmasters.com/courses/frontend-system-design/dom-templating-exercise?t=369)
Document Fragment is lightweight in-memory HTMLElement representation, modifying content doesnt cause reflow, it can be used many times, its isolated from main DOM Tree, you utilize HTML to create markup for component. Branches: (1-dom-begin) y (1-dom-end branch)

### Web APIs for Complex UI Patterns

**Infinite Scroll with IntersectionObserver**

[00:00:28](https://frontendmasters.com/courses/frontend-system-design/infinite-scroll-with-intersectionobserver?t=28)
`git checkout 2-intersection-observer-begin`

[00:05:23](https://frontendmasters.com/courses/frontend-system-design/infinite-scroll-with-intersectionobserver?t=323)
The solution can be found on the [2-intersection-observer-end branch](https://github.com/EvgeniiRay/fundamentals-of-frontend-system-design/tree/2-intersection-observer-end)

**MutationObserver Exercise**

[00:00:06](https://frontendmasters.com/courses/frontend-system-design/mutationobserver-exercise?t=6)
Here's a link to [the CodePen](https://codepen.io/RayEuji/embed/ExJWaEO)

[00:01:50](https://frontendmasters.com/courses/frontend-system-design/mutationobserver-exercise?t=110)
`git checkout 3-mutation-observer-start`

[00:05:29](https://frontendmasters.com/courses/frontend-system-design/mutationobserver-exercise?t=329)
The solutions can be found on the [3-mutation-observer-end branch](https://github.com/EvgeniiRay/fundamentals-of-frontend-system-design/tree/3-mutation-observer-end)

**ResizeObserver**

[00:03:13](https://frontendmasters.com/courses/frontend-system-design/resizeobserver?t=193)
Note: The "when to use" description for Resize Observer should read: "....when running JavaScript code is necessary"

**ResizeObserver Exercise**

[00:00:28](https://frontendmasters.com/courses/frontend-system-design/resizeobserver-exercise?t=28)
`git checkout 4-resize-observer-start`

[00:03:55](https://frontendmasters.com/courses/frontend-system-design/resizeobserver-exercise?t=235)
The solutions can be found on the [4-resize-observer-end branch](https://github.com/EvgeniiRay/fundamentals-of-frontend-system-design/tree/4-resize-observer-end)

### Virtualization

**Virtualization Technique**

[00:03:08](https://frontendmasters.com/courses/frontend-system-design/virtualization-technique?t=188)
`git checkout 5-1-virtualisation-skeleton-start`

[00:03:50](https://frontendmasters.com/courses/frontend-system-design/virtualization-technique?t=230)
Evgenii has created branches and directories for each of these steps

**Handle Top Virtualization**

[00:04:19](https://frontendmasters.com/courses/frontend-system-design/handle-top-virtualization?t=259)
This should be `i--`. Evgenii fixes this later in the lesson.

[00:09:21](https://frontendmasters.com/courses/frontend-system-design/handle-top-virtualization?t=561)
Evgenii added a few `debugger` statements while troubleshooting the issue

### Application State & Network Connectivity

**Network Connectivity**

[00:03:29](https://frontendmasters.com/courses/frontend-system-design/network-connectivity?t=209)
Here's more information about [QUIC](https://quicwg.org/)

[00:06:52](https://frontendmasters.com/courses/frontend-system-design/network-connectivity?t=412)
Here's a link to [the paper](https://onlinelibrary.wiley.com/doi/10.1155/2019/8235458)

**Classic REST & GraphQL**

[00:00:50](https://frontendmasters.com/courses/frontend-system-design/classic-rest-graphql?t=50)
You can find the schema on page 232 of [the slides](https://static.frontendmasters.com/assets/courses/2024-07-23-frontend-system-design/frontend-system-design-slides.pdf)

### Web Application Performance

**CSS, Images & Rendering**

[00:10:43](https://frontendmasters.com/courses/frontend-system-design/css-images-rendering?t=643)
You can find this diagram on page 272 of [the slides](https://static.frontendmasters.com/assets/courses/2024-07-23-frontend-system-design/frontend-system-design-slides.pdf)

### Systems Design Interview: Social Media News Feed

**Requirements & Mock-Up**

[00:00:52](https://frontendmasters.com/courses/frontend-system-design/requirements-mock-up?t=52)
make sure not overcommit on requirements ofr time managements

[00:02:23](https://frontendmasters.com/courses/frontend-system-design/requirements-mock-up?t=143)
first define requirements, and mockup section

[00:03:36](https://frontendmasters.com/courses/frontend-system-design/requirements-mock-up?t=216)
add non functional devices section

[00:06:25](https://frontendmasters.com/courses/frontend-system-design/requirements-mock-up?t=385)
explicacion de como funciona el mockup, posiciones, virtulizacion, viewport, etc. Usa virtualization which involves using absolute positioning, CSS transformations, and registering top and bottom observers. The sliding window is maintained in memory for the visualized list like this: by moving start and end pointers to load new chunks of data while keeping prev loaded data cached in the global state

[00:10:43](https://frontendmasters.com/courses/frontend-system-design/requirements-mock-up?t=643)
explicacion de como se usan los datos

### Wrapping Up

**Wrapping Up**

[00:02:31](https://frontendmasters.com/courses/frontend-system-design/wrapping-up?t=151)
Here's a link to [Evgenii's YouTube Channel](https://www.youtube.com/@FrontEndEngineer)
