### Requirements

- Ubuntu 22.04 installed;
- A network connection;
---

### Installing

- Update the apt package index
```bash
sudo apt-get update
```

- Install the necessary packages
```bash
sudo apt-get install -y ca-certificates curl gnupg lsb-release
```

- Add Docker’s official GPG key
```bash
mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

-  Use the following command to set up the repository
```bash
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

- Install Docker Engine
```bash
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io
```

### Uninstalling

- Stop and remove running containers
```bash
sudo docker rm -f $(docker ps -aq)
sudo docker volume ls | awk 'NR>1 {print $2}' | xargs -n 1 docker volume rm
sudo docker network ls | awk 'NR>4 {print $1}' | xargs -n 1 docker network rm
sudo docker images | awk 'NR>1 {print $3}' | xargs -n 1 docker rmi
```

- Stop the docker.services
```bash
sudo systemctl stop docker.service
```

- Stop and remove docker socket
```bash
sudo systemctl stop docker.socket
sudo rm -rf /var/run/docker.sock
```

- Remove all packages
```bash
sudo apt-get purge -y docker-ce docker-ce-cli containerd.io
sudo apt-get autoremove -y
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
sudo rm -rf /etc/docker
sudo rm -rf /var/run/docker
```

- Delete docker repository
```bash
sudo rm -rf /etc/apt/keyrings/docker.gpg
sudo rm -rf /etc/apt/sources.list.d/docker.list
```

- Delete bridge
```bash
sudo ip link delete docker0
```

- Reset iptables
```bash
sudo iptables -F
sudo iptables -t nat -F
sudo iptables -t mangle -F
sudo iptables -X
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
```

> [!warning]
> Above Iptables rules **can break** some active connections such as SSH.
> Make sure to restart the firewall after paste this commands.


