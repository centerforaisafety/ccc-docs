# Configuration 

## How to install Miniconda or Anaconda
We suggest installing anaconda or miniconda to facilitate installing many other apps on the server. Here’s how we installed miniconda.

```sh
curl https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -o Miniconda3-latest-Linux-x86_64.sh

chmod +x Miniconda3-latest-Linux-x86_64.sh

./Miniconda3-latest-Linux-x86_64.sh
# close and reopen shell or say yes to configure the current shell.
```

Example of how to install [pytorch](https://pytorch.org/get-started/locally/) a popular deep learning library. Similar commands exist for tensorflow etc.

```sh
pip3 install torch torchvision torchaudio
```