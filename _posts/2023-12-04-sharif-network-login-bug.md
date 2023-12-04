---
layout: post
title: Sharif Network Login Bug
slug: sharif-network-login-bug
---

At Sharif University, you should log in to the network to access the internet after connecting to an access point. The login page address is `https://net2.sharif.edu/`. Recently, many students have faced the following error when trying to GET the login page:
```bash
> curl 'https://net2.sharif.edu/'
curl: (7) Failed to connect to net2.sharif.edu port 443 after 3058 ms: Couldn't connect to server
```
Let see what is the IP address of the login server:
```bash
> getent hosts net2.sharif.edu
172.17.1.214    net2.sharif.edu
```
The problem is that the IP address of the login server is in the range that Docker uses for networking, which is `172.17.0.0/16`. So, if you have Docker installed on your machine, your GET request will be routed to the Docker network instead of the university network. To solve this problem temporarily, you can remove the Docker network, but to solve it permanently, you should change the Docker network address. To do so, you can edit the `/etc/docker/daemon.json` (create it if it does not exist) and add the following values:
```json
{
    ...
    "bip": "172.x.0.1/16",
    "default-address-pools": [
        {
            "base": "172.x.0.0/16",
            "size": 24
        }
    ]
}
```
The `x` can be between 0 and 255 (e.g. 18).
Then restart the Docker service:
```bash
> sudo systemctl restart docker
```
Now, the Docker network will not conflict with the university network.
