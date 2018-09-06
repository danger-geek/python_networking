# python_networking
Collection of scripts and examples of Python code, libraries, and utilities for working with Network Devices.  

> This repo is an active work in progress.  

# Setting Up to Run Examples 
## Clone and Prep the Environment
1. Clone the code repo

```bash
git clone https://github.com/hpreston/python_networking
cd python_networking
```

1. Setup Python Virtual Environment.  

```bash
python3.6 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

## Infrastructure Resources
The example scripts for `data_manipulation` require nothing other than the files in this repository and the Python libraries installed with `pip install` above.  

The example scripts for `device_apis` & `network_testing` leverage DevNet Always On Sandboxes that are publicly available, with no VPN connection needed.  The details for these infrastructure are included in the scripts.  

## Infrastructure for Configuration Management Demonstrations
The configuration management scripts in this repository are written to target a sample network topology built as Core > Dist > Access with IOS XE devices in the Core, and NX-OS devices for Dist and Access.  The demo network can be run with Cisco VIRL or CML, and the [`topology.virl`](topology.virl) file in the repo has the details.  If you do not have your own VIRL server, you can reserve a free [DevNet Multi-IOS VIRL Sandbox](https://devnetsandbox.cisco.com/RM/Diagram/Index/6b023525-4e7f-4755-81ae-05ac500d464a?diagramType=Topology) to use.  

1. After connecting to the Sandbox with VPN, start the development network.  This single line command will start the simulation, wait to completely start, and then lay down an initial configuration with Ansible.  

```bash
virl up --provision \
  && virl generate ansible -o setup/default_inventory.yaml \
  && cd setup \
  && ansible-playbook network_deploy.yaml \
  && cd ../
```
