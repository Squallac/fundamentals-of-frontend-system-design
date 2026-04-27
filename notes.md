# Box Model

Box properties: Block size y block type

# Browser formatting context

Cuando un elemento nuevo es creado, entra al formatting context actual, si ese elemento lleva estilos, se crea un nuevo formatting context isolado. Por ejemplo los spans crean inline formatting context de manera implicita.

3 key ideas

1. Isolation: Elements within the context are shielded from external rules,
2. Scalability: New rule sets can be introduced by creating a new context,
3. Predictability: A strict set of rules allows for consistent element positioning

The block formatting context is set by default when an HTML page is initiated
