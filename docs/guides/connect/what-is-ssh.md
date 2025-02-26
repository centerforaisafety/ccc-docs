# SSH 

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

### What’s next?

In our guide How to use SSH keys, learn how to generate an public/private key pair and use it to connect to the cluster.