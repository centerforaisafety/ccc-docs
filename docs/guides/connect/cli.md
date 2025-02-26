# Connect to the cluster

## **Connect with the command line**

Use your private key to authenticate when connecting to a running instance via SSH. The instance has an SSH key associated with it, provided when that instance was created. The private key must correspond to that SSH key.

=== "Connect to the login node with SSH"
    ```sh
    ssh -i <path_to_your_private_key> <username>@<ip_address>
    ```

Examples:

=== "Ed25519"

    ```sh
    ssh -i ~/.ssh/id_ed25519 john_smith@compute.safe.ai
    ```
    
=== "RSA"

    ```sh
    ssh -i ~/.ssh/id_rsa john_smith@compute.safe.ai
    ```