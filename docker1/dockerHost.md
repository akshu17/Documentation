## 2. Host

This driver removes the network isolation between Docker and the host.  
The containers are directly connected to the host machine network without an extra layer of any Docker network.  
They share the same TCP/IP stack and the same namespace of the host machine.  
All the network interfaces present on the host machine are accessible by this container.

### Network Namespace Sharing
The container shares the same network namespace as the host.  
It can directly access the network interfaces and services available on the host without any additional isolation.

### Port Binding
Ports exposed by the container are directly bound to the host's network interfaces.  
This means that services running within the container can be accessed on the same ports as if they were running on the host.

### Host's IP Address
The container uses the host's IP address, making it appear as if the container's services are running on the host itself.
