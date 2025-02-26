# Configuration

## How to switch your shell
Add the following to the end of your `.bashrc` file to which shell you'd like to run.
The different shells are by default installed into `/usr/bin/`.
```sh
# To switch to zsh
if [ "$SHELL" != "/usr/bin/zsh" ]
then
    export SHELL="/usr/bin/zsh"
    exec /usr/bin/zsh
fi
```
!!! tip "If your favorite shell is not installed on the system just ask an admin to add it for you."