# Custom Bridge in Docker

A **custom bridge network** in Docker allows you to create your own isolated network with specific settings instead of using Docker’s default bridge. This is useful when you want better control over container networking, like assigning fixed subnets, IP ranges, or enabling container name resolution within the network.

---

## Why Create a Custom Bridge?

- Isolate groups of containers from others.
- Control IP addressing and subnet.
- Enable automatic DNS resolution (containers can talk by name).
- Customize network driver options.

---

## How to Create and Use a Custom Bridge Network

1. **Create the Custom Bridge Network**

Example:

```bash
docker network create \
  --driver bridge \
  --subnet 192.168.100.0/24 \
  custom-bridge-network
