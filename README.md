# RISC-V GDB Environment for CSC3060 Bomblab

## Docker

In this tutorial, we will use a prebuilt Docker image to ensure a consistent, reproducible environment for doing the bomblab. 

Before starting, make sure you have installed Docker and any other necessary packages. 

## Environment Setup

The Docker image has been built for both x86_64 and ARM64, so the same instructions here will work for all systems (Apple/AMD/Intel).

```bash
#1. Pull Docker image from ghcr.io
docker pull ghcr.io/lwh1/rvemu:latest

# 2. Run container
docker container run --name rvemu -p 2222:2222 -d ghcr.io/lwh1/rvemu

# 3. SSH into QEMU
ssh root@localhost -p 2222

# When prompted for password, enter: csc3060
# You are now connected to your RISC-V environment
```

### Starting and stopping your container

After the initial setup, you can start and stop with its assigned name

- **Start:** `docker container start rvemu`
- **Stop:** `docker container stop rvemu`

## Optional Setup

#### SSH key authentication

```bash
# Setup SSH key authentication
ssh-keygen
ssh-copy-id -p 2222 -f -i ~/.ssh/id_rsa.pub root@localhost
# When prompted for password, enter: csc3060
```

SSH key authentication is a quality of life feature that you can use to securely login to a remote server password-free. In this case, our *"remote server"* is our not so remote QEMU machine inside the container.

#### SSH config

Setting up a SSH config lets you login to a host without typing in the host IP address, port, and username. Using the config below, you can login by using `ssh debian-rv64`

```bash
# Setup SSH config
echo "
Host csc3060
   HostName 127.0.0.1
   User root
   Port 2222
" >> ~/.ssh/config
```

You can copy and paste the above into your bash shell to add the SSH config.
