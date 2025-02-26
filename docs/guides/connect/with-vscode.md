# Connect to the cluster

## **With VSCode**

???+ Warning
    Please do not run heavy computations on the login node. This includes installing things (request a CPU node to do so).

    Below is a cleaned-up, more structured explanation of using VS Code on the CAIS cluster. Adjust paths, node names, or any settings specific to your environment as needed.

This guide explains how to use Visual Studio Code (VS Code) for remote development on the CAIS cluster. It covers performance considerations, recommended settings, and the two primary remote extensions: `Remote - SSH` and `Remote - Tunnels`.

!!! warning "Performance Considerations"

	-	CPU Usage: Some AI-powered extensions (e.g., TabNine, GitHub Copilot) can consume noticeable CPU resources. While this is not currently a problem, we may have to disable these if overall usage becomes too large.
	-	RAM Usage: VS Code’s main performance impact on the cluster is memory consumption, which depends heavily on:
	-	Number of installed extensions (more than ~10 can noticeably impact responsiveness).
	-	Size of the working directory you have open in VS Code.

!!! tip "Recommendation:"

	-	Keep your extension list lean. Uninstall or disable extensions you rarely use.  
	-	Open only the necessary subdirectories rather than your entire home folder or project tree.  

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
	    -	Follow the basic SSH setup to ensure you can ssh to your cluster (e.g., ssh cais_cluster or ssh <username>@compute.safe.ai).
	    -	If you have an ~/.ssh/config file, VS Code will detect any hosts listed there.
	3.	Enable remote.SSH.remoteServerListenOnSocket
	    -  	Open VS Code Settings (Ctrl+, or ⌘+,) and search for remote.SSH.remoteServerListenOnSocket.
	    -	Check (enable) this option. It’s disabled by default.
	    -  	This ensures a more stable, socket-based communication between your local VS Code client and the cluster.
	4.	Connect to the Cluster
	    -	Press F1 (or Ctrl+Shift+P/⌘+Shift+P) to open the Command Palette.
	    -	Type Remote-SSH: Connect to Host..., and select your configured SSH host (e.g., cais_cluster).
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

### **Summary**

-	Install minimal extensions: Keep only what you need to reduce memory usage.
-	Use Remote - SSH or Remote - Tunnels: Both provide a smooth experience; pick whichever fits your workflow.
-	Monitor resource usage: AI extensions can be CPU-intensive, and large projects or many extensions can impact RAM usage on the cluster.

These steps should help you set up VS Code for remote development on the CAIS cluster without unnecessary overhead or performance issues.