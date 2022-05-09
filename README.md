## Elk Stack Project
Files in this repository pertain to the project described in this Readme 

### Creating a Virtual Environment
 #### Create a new resource group
    - Default region
    - Named RedTeam in this project
    
 #### Add a new virtual network to the resource group
    - Default settings
    - Named RedTeam-Net in this project
    
 #### Protecting the virtual network with a firewall
    - Create a network security group
    - Named RedTeam-SecurityGroup in this project
    - Edit inbound rules for the NSG
    - Allow RDP on port 3389 by creating a new rule.
    - Source: Host machine IP address
    - Source Port ranges: Leave the * to signify all source ports
    - Destination: VirtualNetwork
    - Service: RDP
    - Destination Port Ranges: 3389
    - Protocol: TCP
    - Action: Allow
    - Priority: 500
    - Description: "Allow-RDP"
   
### Adding Virtual Computers
  #### Creating the Jump Box
    - Create new virtual machine in the RedTeam resource group
    - Same region as resource and security group
    - Create an SSH key for remote connections
    - Choose VM Size - Standard B1s - 1 CPU, 1 GB RAM
    - Make sure VM is in the correct security group
    - Make sure VM has a static public IP address
   
  #### Creating the web VMs
    - Create an additional 2 VMs
    - RedTeam resource group
    - Same region as resource and security group
    - Use the SSH key that was created for the jump box
    - Sizes should be Standard - B1ms
    - Ensure both VMs are in the same availibility set
    - Ensure both VMs are in the correct security group
    - Ensure both VMs do not have public IP addresses
    - VMs are named Web-1 and Web-2 in this project
   
  #### Allowing SSH from host machine to jump box
    - Add an inbound security rule to the security group
    - Source: Host machine IP address
    - Source Port ranges: Leave the * to signify all source ports
    - Destination: IP address of  jump box
    - Service: SSH
    - Destination Port Ranges: 22
    - Protocol: TCP
    - Action: Allow
    - Priority: 501
    - Description: "Allow SSH from my IP"
    
 #### Configuring jump box to run Docker containers
    - SSH into the jump box
    - run sudo apt update
    - run sudo apt install docker.io
    - run sudo systemctl status docker
    - run sudo docker pull cyberxsecurity/ansible
    - run sudo su
    - run sudo docker run -cyberxsecurity/ansible:latest bash
  
 #### Creating a security group rule to allow full vNetwork access to the jump box
    - Source: Jump box IP address
    - Source Port ranges: *
    - Destination: VirtualNetwork
    - Service: SSH
    - Destination Port Ranges: 22
    - Protocol: TCP
    - Action: Allow
    - Priority: 502
    - Description: "Allow SSH from my IP"
    
 #### Creating an Ansible playbook to configure VMs with the Damn Vulnerable Web App
    - Connect to the jump box and connect to the Ansible container
    - 

### ELK Installation on Azure Virtual Network
  
 #### Create a new vNet using the same resource group
    - New Region, not the same as other VMs
    - Default settings
    - named Project1VNet in this project
    
 #### Create a peer connection between vNets
    - Under settings, select 'Peerings'
    - Add new peering with a unique name that describes the connection between vNets
    - Remember to also add the peering for the original vNet to the new vNet
  
 #### Create a new Ubuntu VM
    - 4 GB+ of RAM
    - At least 4 GiB of memory
    - Must have a public IP Address
    
