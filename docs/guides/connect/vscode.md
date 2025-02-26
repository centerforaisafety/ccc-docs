# Connect to the cluster

## **How to connect with VSCode**

This guide explains how to use Visual Studio Code (VS Code) for remote development on the CAIS Compute Cluster. It covers performance considerations, recommended settings, and the two primary remote extensions: `Remote - SSH` and `Remote - Tunnels`.

### **Remote Extensions Overview**

There are two primary ways to develop remotely using VS Code:

	1.	Remote - SSH Extension
	2.	Remote - Tunnels Extension

Both deliver nearly identical development experiences in VS Code; they differ only in how they connect to the server. Choose whichever best fits your workflow.

### **Using the Remote - SSH Extension**

!!! instructions
	1.	Install the extension
        - In VS Code, open the Extensions panel (Ctrl+Shift+X or ⌘+Shift+X) and search for Remote - SSH.
	2.	Configure SSH
	    -	Follow the basic SSH setup to ensure you can ssh to your cluster (e.g., ssh cais_cluster_alias or ssh username@compute.safe.ai).
	    -	If you have an ~/.ssh/config file, VS Code will detect any hosts listed there.
	3.	Enable remote.SSH.remoteServerListenOnSocket
	    -  	Open VS Code Settings (Ctrl+, or ⌘+,) and search for remote.SSH.remoteServerListenOnSocket.
	    -	Check (enable) this option. It’s disabled by default.
	    -  	This ensures a more stable, socket-based communication between your local VS Code client and the cluster.
	4.	Connect to the Cluster
	    -	Press F1 (or Ctrl+Shift+P/⌘+Shift+P) to open the Command Palette.
	    -	Type Remote-SSH: Connect to Host..., and select your configured SSH host (e.g., cais_cluster_alias).
	5.	Open or Create a Project
	    -	Once connected, you can open a folder on the remote machine or create a new one.
	    -  	Install any necessary extensions on the remote side when prompted (VS Code will ask to install or “reload” them).

That’s it! You can now develop on the cluster as if it were a local environment, with code-completion, integrated terminal, debugging, etc.

### **Using the Remote - Tunnels Extension**
The Remote - Tunnels extension allows you to run VS Code in the browser or desktop client without needing direct SSH from your local VS Code. It can be more convenient for connecting to an interactive Slurm session on a compute node.

!!! Instructions

	1.	Install the extension
	    -	In VS Code, open Extensions and search for Remote - Tunnels.
	2.	SSH into the Cluster
	    -	From a terminal (outside of VS Code), ssh cais_cluster (or ssh <username>@compute.safe.ai).
	    -	We strongly encourage running commands from your /data/<username> directory to ensure the correct privacy permissions for any folders VS Code creates.
	3.	Start the Tunnel
	    -	Once logged in, run the code tunnel command (or similar command that the Remote - Tunnels documentation provides).
	    -	You’ll see instructions and a URL to open the remote environment.
	4.	Open VS Code or Browser
	    -	If you’re using the desktop VS Code client, enter the provided code to authenticate and connect.
	    -	If you’re using the browser, open the provided URL in your web browser to access the remote environment.
	5.	(Optional) Interactive Node
	    -	If you plan to work on a compute node rather than the login node, you can request an interactive session (srun --pty bash) and then run the code tunnel command there. This ensures your code execution is on the compute node itself.