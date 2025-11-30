
🧪 Arista ContainerLab Lab Series

Build, Mount, and Run Arista EOS Labs Using ContainerLab, OrbStack, and VS Code

This repository contains all files used in the video series on building an Arista ContainerLab environment on macOS or Windows using OrbStack, VS Code, and Arista cEOS images. Each video builds on the previous one, guiding you from installation to deploying full topologies.

⸻

📺 Video Series Overview

⸻

1. Install OrbStack & ContainerLab

This video walks you through installing OrbStack, configuring a Linux VM, allocating system memory, and installing ContainerLab along with Docker.

Steps Covered
	1.	Download OrbStack:
https://orbstack.dev/download
It auto-detects your OS and provides the correct installer.
	2.	Install OrbStack and move it into Applications (Windows users follow the on-screen installer).
	3.	When prompted to create a VM, choose Linux.
	4.	If no Linux VM appears:
	•	Go to Machines → New Machine
	•	Name it ContainerLab
	•	Choose Debian (default settings)
	5.	Stop the VM → Right-click → Make Default
	6.	Open OrbStack Settings → System → Memory Limit
	•	Set VM memory to at least 8GB
	•	More memory = more network devices
	•	If memory is limited, you will rely on the delay setting inside your topology file.
	7.	Start the VM and open its Terminal tab.
	8.	Install ContainerLab:

curl -sL https://containerlab.dev/setup | sudo -E bash -s "all"


	9.	Verify tools:

clab version
docker --version



⸻

2. Connect VS Code to Your OrbStack VM & Mount a Local Folder

This video teaches you how to connect VS Code to your OrbStack VM using Remote Explorer and properly mount a lightweight folder to avoid memory overhead.

Steps Covered
	1.	Open VS Code.
	2.	Install the Remote Explorer extension from Microsoft.
	3.	A new sidebar icon appears for the extension.
	4.	Click the bottom-left >< icon → Remote Window → SSH: Connect to Host
Select orb.
(If “orb” does not appear, confirm the VM is running.)
	5.	Create a lightweight directory on your local system:
Recommended: /Users/your_account/Labs
	•	Avoid mounting heavy folders like Documents or Downloads — they consume excessive RAM.
	•	Copy the Arista folder from this GitHub repository into Labs.
	6.	In VS Code:
	•	Go to the Explorer sidebar
	•	Choose Open Folder
	•	Remove the default Linux VM path
	•	Type /Users/... to navigate to your local Labs folder
	•	Select the folder and click OK
	7.	You are now mounted into the VM.
Verify:

clab version


	8.	Download your Arista cEOS image (you’ll need it for the next video).

⸻

3. Create a Docker Image from the Arista cEOS File

This video shows how to build the required Docker image from your cEOS image.

Steps Covered
	1.	Download your Arista cEOS image (must be obtained directly from Arista due to licensing).
	2.	Place the file into:
/Users/yourname/Labs/Arista/images
	3.	Open VS Code, ensure you are connected to orb with the folder mounted.
	4.	Confirm connectivity:

clab version


	5.	Build the Docker image:

cd Arista
ls -al      # confirm expected directory structure
docker import images/cEOS ceos:4.30.1F

	•	The tag (e.g., 4.30.1F) must match your downloaded cEOS version.

	6.	Verify the imported image:

docker images



⸻

4. Understanding the ContainerLab Topology File

This video explains the structure of the topo.clab.yaml file and best practices for memory and configuration.

Topics Covered
	•	File name: topo.clab.yaml
	•	ContainerLab uses this file to build your lab.
	•	Three major sections:
	1.	name
	2.	mgmt
	3.	topology
	•	Memory and startup delay:
	•	If VS Code disconnects, the VM may be out of RAM
	•	Increase memory in OrbStack OR increase delay: in the topology file
	•	The init-configs directory provides base switch configurations
	•	Port forwarding is defined in the topology file to allow local access
	•	Verification of link definitions and topology layout

⸻

5. Deploying the ContainerLab Topology

This video walks through launching the lab using your topology file.

Steps Covered
	1.	Stay in VS Code connected to orb.
	2.	Confirm your local folder is mounted so ContainerLab can read the YAML file.
	3.	Deploy with:

sudo clab deploy -t topo.clab.yaml


	4.	ContainerLab will:
	•	Start the VM devices
	•	Apply delay values to manage memory
	•	Load your init-configs
	•	Display a final table of device names and management IPs
	5.	Once complete, access devices via:
	•	SecureCRT
	•	Any SSH client
	•	OrbStack CLI
	•	localhost or 127.0.0.1 (thanks to port forwarding)
	6.	Next video will cover accessing switches via SSH.

⸻

📁 Repository Structure

labs/
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

Follow the videos in order—each builds on the last.
	1.	Install OrbStack & ContainerLab
	2.	Connect VS Code and mount local folder
	3.	Create Docker image from cEOS
	4.	Review topology file
	5.	Deploy your lab

⸻

👍 Support the Project

If you’re learning from this series, consider liking or subscribing on YouTube.
Open issues or discussion threads here if you need help.

⸻

If you’d like, I can also:
✅ Add a Table of Contents
✅ Add badges (YouTube, GitHub Repo, etc.)
✅ Add screenshots or diagrams
Just tell me!
