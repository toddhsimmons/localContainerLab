
🧪 Arista ContainerLab Lab Series

Build, Mount, and Run Arista EOS Labs Using ContainerLab, OrbStack, and VS Code

This repository contains all files used in the video series on building an Arista ContainerLab environment on macOS or Windows using OrbStack, VS Code, and Arista cEOS images. Each video builds on the previous one, guiding you from installation to deploying full topologies.

⸻

📺 Video Series Overview

⸻

1. Install OrbStack & ContainerLab

This video walks you through installing OrbStack, configuring a Linux VM, allocating system memory, and installing ContainerLab along with Docker.

Steps Covered
	1.	Download OrbStack: https://orbstack.dev/download, It auto-detects your OS and provides the correct installer.
	2.	Install OrbStack and move it into Applications (Windows users follow the on-screen installer).
	3.	When prompted to create a VM, choose Linux.
	4.	If no Linux VM appears:
      •	Machines → New Machine
      •	Name: ContainerLab
      •	Distribution: Debian (default)
	5.	Stop the VM → Right-click → Make Default.
	6.	Open OrbStack Settings → System → Memory Limit:
      •	Set memory to at least 8GB
      •	More memory = more devices
      •	If memory is low, you’ll rely on the delay option inside the topology file
	7.	Start the VM and open the Terminal tab.
	8.	Install ContainerLab:  curl -sL https://containerlab.dev/setup | sudo -E bash -s "all"
	9.	Verify installation:
      clab version
      docker --version


⸻

2. Connect VS Code to Your OrbStack VM & Mount a Local Folder

This video shows how to connect VS Code to your OrbStack VM using Remote Explorer and mount a local directory safely.

Steps Covered
	1.	Open VS Code.
	2.	Install the Remote Explorer extension (Microsoft).
	3.	A new sidebar icon for Remote Explorer appears.
	4.	Click the bottom-left >< icon → Remote Window → SSH: Connect to Host → select orb (If “orb” isn’t listed, ensure the VM is running.)
	5.	Create a lightweight folder on your Mac/PC:  Recommended: /Users/your_account/Labs
      •	Avoid Documents or Downloads (too many nested files = RAM issues)
      •	Copy the Arista folder from this GitHub repo into Labs
	6.	In VS Code:
      •	Open the Explorer sidebar
      •	Click Open Folder
      •	Clear the default Linux VM path
      •	Type /Users/... and navigate to your Labs folder
      •	Select it and click OK
	7.	You are now mounted into the VM.
      Verify:  clab version
	8.	Download your Arista cEOS image (needed for the next video).

⸻

3. Create a Docker Image from the Arista cEOS File

This video explains how to take your cEOS file and import it as a Docker image for ContainerLab.

Steps Covered
	1.	Download your Arista cEOS image (must be obtained directly from Arista).
	2.	Place the downloaded file into:  /Users/yourname/Labs/Arista/images
	3.	Open VS Code and ensure you’re connected to orb with the local folder mounted.
	4.	Verify the environment:
      clab version
	5.	Build the Docker image:
      cd Arista
      ls -al
      docker import images/cEOS ceos:4.30.1F (Replace 4.30.1F with your exact cEOS version)
	6.	Verify the new image:
      docker images


⸻

4. Understanding the ContainerLab Topology File

This video walks through the structure and purpose of the topo.clab.yaml file.

Topics Covered
	Topology file: topo.clab.yaml Used by ContainerLab to build the full lab
	Three major sections:
	1.	name
	2.	mgmt
	3.	topology
	•	If VS Code disconnects, your VM is likely out of RAM
	•	Increase memory or increase the delay value
	•	init-configs folder provides base switch configuration
	•	Port forwarding allows local SSH access via localhost
	•	Verification of links & node definitions

⸻

5. Deploying the ContainerLab Topology

This video shows how to launch the lab once your topology file and Docker image are ready.

Steps Covered
	1.	Ensure VS Code is connected to orb.
	2.	Confirm your local folder is mounted so ContainerLab can access topo.clab.yaml.
	3.	Deploy the lab:  sudo clab deploy -t topo.clab.yaml
	4.	During deployment ContainerLab will:
      •	Start devices
      •	Apply delay settings
      •	Load init-configs
      •	Display a device table with management IP addresses
	5.	Access devices using:
      •	SecureCRT
      •	Any SSH client
      •	OrbStack CLI
      •	localhost or 127.0.0.1 (via port forwarding)
	6.	The next video demonstrates several ways to SSH into the devices.

⸻

📁 Repository Structure

Labs/
└── Arista/
    ├── topo.clab.yaml        # ContainerLab topology file
    ├── init-configs/         # Base device configs for startup
    ├── images/               # Place your cEOS image here
    └── scripts/              # Optional automation utilities
README.md

⸻

⭐ Requirements
	•	OrbStack
	•	VS Code + Remote Explorer
	•	ContainerLab
	•	Docker
	•	Arista cEOS image (download from Arista portal)

⸻

🚀 Getting Started

Follow the videos in order—each builds on the previous one:
	1.	Install OrbStack & ContainerLab
	2.	Connect VS Code and mount your local folder
	3.	Import the Docker image for cEOS
	4.	Review the topology file
	5.	Deploy your lab

⸻

👍 Support the Project

If you’re learning from this series, consider liking or subscribing on YouTube.
Feel free to open issues or discussions here on GitHub if you need help.

⸻

If you’d like:
✅ A Table of Contents
✅ GitHub badges
✅ Screenshots / diagrams
Just tell me — I can generate them!
