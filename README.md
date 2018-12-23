# Arm Cluster

## Goal 
Have a low budget docker cluster running on Arm 

### Why 
- Just to prove that I'm capable
- Reduce power consumption of the current setup (2 x86 machines)

## Recipe
This is just a list of what I did...

### Hardware
| Qtd           | Item                                                          | Price (aprox)  |
| ------------- |:--------------------------------------------------------------| --------------:|
| 1             | [X96 Mini TV Box 2GB RAM + 16GB ROM](https://bit.ly/2Gz0gVq)  | 29.30€         |
| 1             | [Class 10 Micro SDCard](https://bit.ly/2Rexsp7)               | 4.92€          |

### Instructions

#### Base System
- Install the Base System (ArmDebian)  
    - Follow these [instructions](https://forum.armbian.com/topic/7930-armbian-for-amlogic-s9xxx-kernel-41x-ver-555/)
    - And check out this [comment](https://forum.armbian.com/topic/7930-armbian-for-amlogic-s9xxx-kernel-41x-ver-555/?page=8&tab=comments#comment-66454)
        -   The dtb for X96 Mini is the 
            `meson-gxl-s905x-khadas-vim.dtb` 
- Set the Password, 
- Change the hostname [instructions](https://www.cyberciti.biz/faq/ubuntu-change-hostname-command/)
- Set a fixed IP - [instructions](https://linuxconfig.org/how-to-setup-a-static-ip-address-on-debian-linux)
- The system should be operational 
- ```systemctl disable haveged.service```

#### Docker 
- Docker (Default installation)
    - In doubt follow these  [instructions](https://blog.alexellis.io/getting-started-with-docker-on-raspberry-pi/)
- Swarm 
    - If 1st machine:
        - Create a Docker Swarm [instructions](https://docs.docker.com/engine/reference/commandline/swarm_init/)
            ```
            docker swarm init
            ```
    - Other Machines
        - Add to the existing Swarm
            ```
            docker swarm join --token {YOURTOKEN} {IP}:2377
            ```
#### Portainer (this is only done once)
- Install Portainer to Swarm Administrtion 
    - Follow the **Manage a LINUX Swarm cluster with Portainer Server and the Portainer Agent** topic
        - [Instructions](https://www.portainer.io/installation/)
- Access the Browser on the url
    - http://{IP}:9000
- Follow the creation of the initial administrator user. 


### TODO
- [x] Build the setup
- [x] Create the docker swarm
- [x] Administrate docker swarm via Portainer
- [] Migrate Current HomeAssistant Stack to Cluster 
