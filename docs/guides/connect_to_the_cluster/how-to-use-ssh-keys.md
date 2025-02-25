# SSH

## **How to use SSH keys**

Connect to the login node using an SSH key

You must provide an SSH key when you request access to the cluster. Once access has been granted, that SSH key is used to authenticate for remote command-line access to the login node.

### **Generate a public/private key pair**

!!! Info
    We support OpenSSH public key formats:

    - ssh-ed25519
    - ssh-rsa

If you already have a public/private key pair of a supported format, you can use that pair instead of generating a new one.

Follow the steps below to generate a key pair with a command-line tool called `ssh-keygen`. This tool is pre-installed on nearly all operating systems.

Use any supported format for your key pair. The tabs below contain instructions for generating a key pair with either the Ed25519 algorithm or RSA algorithm.

??? question "How to create an SSH key pair?"
    === "ED25519"

        ```sh
        # Generate the key pair 
        ssh-keygen -t ed25519 -C "your_email@example.com"
        # If prompted to enter a filename, press `Enter` to save the key pair to the default location (`~/.ssh/`). 
        # When prompted to enter a passphrase, you can optionally do so to increase secruity.
        ```

        ```sh
        # Confirm that your key pair was created
        ls ~/.ssh
        ```

        ```sh
        # View your public key
        cat ~/.ssh/id_ed25519.pub
        ```

    === "RSA"

        ```sh
        # Generate the key pair
        ssh-keygen -C "your_email@example.com"
        # If prompted to enter a filename, press `Enter` to save the key pair to the default location (`~/.ssh/`). 
        # When prompted to enter a passphrase, you can optionally do so to increase secruity.
        ```

        ```sh
        # Confirm that your key pair was created
        ls ~/.ssh
        ```

        ```sh
        # View your public key
        cat ~/.ssh/id_rsa.pub
        ```

???+ Warning
    With any public/private key pair that you generate, your public key can be shared freely. Your private key should be just that—private! Take care not to share it with others, or in public repositories such as in GitHub.

### **Add an SSH key**

If you don’t have a public key, see: Generate a public/private key pair.

!!! Tip
    Modifying the `~/.ssh/authorized_keys` incorrectly could disable SSH access to the login. Please ask an admin for assistance.

### **View existing SSH keys**

```sh
cat ~/.ssh/authorized_keys
```



### **Delete an SSH key**

???+ Warning
    Deleting an SSH key removes the ability to authenticate to the login node with that key. Please ask an admin for assistance.

### **Connect to the login node with an SSH key**

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