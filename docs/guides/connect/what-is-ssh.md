# Connect to the cluster

## **What is SSH?**

### **The Secure Shell (SSH) protocol**

SSH is a cryptographic network protocol used for secure access to a networked computer. The data transmitted between the client and server is protected with strong encryption algorithms, ensuring privacy and data integrity.

All compute nodes on the cluster run SSH servers for remote access. These servers authenticate using SSH keys.

### **About SSH keys**

For improved security, we use [public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) for authentication instead of a password. This is also known as SSH key authentication. This method requires that you provide your own public/private key pair.

Your public key is stored in your home directory `~/.ssh/authorized_keys`. Its corresponding private key is stored locally on the computer that you use to access your instance. SSH access is granted by verifying that your private key corresponds to the public key. As an analogy, think of a public key as a lock that only your private key can unlock.

!!! Tip
    Public/private key pairs are used for many purposes, not only SSH. For example, they are used in file encryption, digital signatures, and cryptocurrency transactions.

### **SSH clients**

An SSH client is used to remotely connect to an instance. Nearly all computers have an SSH client installed by default. To test if you have one installed, enter the following command in your CLI shell:

```sh
ssh -v
```

You should see a list of usage options. If you see an output indicating that the command was not found, install an SSH client. Two popular options are OpenSSH and Putty.

### **Create an SSH key pair**
If you already have a public/private key pair of a supported format, you can use that pair instead of generating a new one.

Follow the steps below to generate a key pair with a command-line tool called `ssh-keygen`. This tool is pre-installed on nearly all operating systems.

Use any supported format for your key pair. The tabs below contain instructions for generating a key pair with either the Ed25519 algorithm or RSA algorithm.

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