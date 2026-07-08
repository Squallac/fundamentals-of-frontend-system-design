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

coding branch `2-intersection-observer-begin`