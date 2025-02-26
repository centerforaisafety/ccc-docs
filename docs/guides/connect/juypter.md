# Connect to the cluster

## **How to connect with Jupyter**

!!! info "Prerequisites"
    - You can SSH into the cluster (e.g. ssh username@compute.safe.ai).
    - Anaconda (or another Python environment) installed.  

### **Connect to the Cluster**

```sh
ssh -i ~/.ssh/id_ed25519 <username>@compute.safe.ai
```

### **Install or Confirm Jupyter is Installed**

Make sure Jupyter is available in your environment:
```sh
# If using conda
conda install -c anaconda jupyter

# Alternatively, using pip
pip install jupyter
```
### **Request an Interactive CPU Node**

From the login node, run:
```sh
srun --pty bash
```
This gives you an interactive shell on one of the compute nodes. Note which node you landed on (it might be something like `compute-permanent-node-###`).

### **Start Jupyter on the Compute Node**

Once you’re on the compute node, set up a random port and start Jupyter:
```sh
# Unset this variable if set, to avoid issues
unset XDG_RUNTIME_DIR

# Export a random port above 1024
export NODEPORT=$(( $RANDOM + 1024 ))
echo "Using port $NODEPORT"

# Launch Jupyter without opening a browser
jupyter notebook --no-browser --port=$NODEPORT
```
!!! info "Keep track of:"
  
	1.	The port number you see in `$NODEPORT`.  
	2.	The notebook URL that Jupyter prints out (something like `http://localhost:19303/?token=...`).

Leave this terminal open while Jupyter runs.

### **Set Up SSH Tunneling from Your Local Machine**

Open a new terminal on your local machine (not the compute node) and run:
```sh
# Example: If NODEPORT=19303 and your node is "compute-permanent-node-123"
export NODEPORT=19303

ssh -t -t cais_cluster -L ${NODEPORT}:localhost:${NODEPORT} \
    ssh -N compute-permanent-node-123 \
    -L ${NODEPORT}:localhost:${NODEPORT}
```
!!! info "Explanation:"

    -   The first SSH command connects you to the cluster’s login node.  
    -   The second SSH command (nested inside) connects you from the login node to the compute node, while setting up port forwarding so that traffic on localhost:$NODEPORT flows to the Jupyter process.

## **Open Jupyter Notebook in Your Browser**

Finally, open your preferred browser on your local machine and paste in the notebook link you copied from step 4. For example:
```sh
http://localhost:19303/?token=cb2b708e5468268ase8c46448fc28e78bd049a977cdcbd65d1
```
That’s it! You should now see the Jupyter Notebook interface running on the compute node, but accessible in your local browser. You can run notebooks as normal, including CPU- or GPU-based workloads as permitted by the node you requested with srun.

!!! tip "Troubleshooting"

	-	Port Already in Use: If you see an error about the port already in use, run the steps again with a different random port or specify export NODEPORT=##### manually.  
	-	SSH Config: If your SSH setup differs, adjust commands to use an alias if you have one.  
	-	Environment Issues: Ensure that your Python environment is loaded before running jupyter notebook.