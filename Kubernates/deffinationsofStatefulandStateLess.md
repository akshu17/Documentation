## Definitions: Stateful vs Stateless

### ✅ Stateless Application — Definition

A **Stateless application** does not store any session or client data on the server between requests. Each request is handled independently and has all the information needed to process it.

**Example:** A typical web frontend or REST API.

### ✅ Stateful Application — Definition

A **Stateful application** keeps track of client state or stores data that must persist between requests or sessions. The server remembers information about previous interactions.

**Example:** A database server, message queue, or any service that stores user sessions.

**Key Difference:** Stateless apps are easy to scale and replace. Stateful apps need stable identity and persistent storage.
