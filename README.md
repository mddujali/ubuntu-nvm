# Setup Node Version Manager (NVM) in Ubuntu Desktop 16.04 or Higher

## Requirements

- Git v1.7+

## Installation

### Clone this repo in the root of your user profile
```console
$ cd
$ git clone https://github.com/creationix/nvm.git .nvm
```

### Now add these lines to your ~/.bashrc, ~/.profile, or ~/.zshrc file to have it automatically sourced upon login: (you may have to add to more than one of the above files)
```plain
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

### To download, compile, and install the latest release of node, do this:
```console
$ nvm install node
```

### To install a specific version of node:

```console
$ nvm install 6.14.4 # or 10.10.0, 8.9.1, etc
```

> **Note:** The first version installed becomes the default. New shells will start with the default version of node (e.g., `nvm alias default`).

### You can list available versions using ls-remote:
```console
$ nvm ls-remote
```

### And then in any new shell just use the installed version:
```console
$ nvm use node
```

### You can also get the path to the executable to where it was installed:
```console
$ nvm which 9.2.0
```

### Set default version:
```console
$ nvm alias default 9
```

### NVM is great and makes switching between node versions easy and convenient. However, there's one caveat. If you type:
```console
$ which node
```

> **Note:** You will see something interesting. Nvm installs node.js inside your user's home directory. This is fine for development, but if you want to actually host node applications, you don't want to install the latest new version of node via nvm and discover that you've inadvertently caused your production node app (which can be incompatible with the latest node.js) to stop working. It's best to install one copy of node globally so that other users can access it, and use nvm to switch between your development versions.

### To do this, run the following command (entering your user's password at the prompt):
```console
$ n=$(which node);n=${n%/bin/node};chmod -R 755 $n/bin/*;sudo cp -r $n/{bin,lib,share} /usr/local;
```

The above command is a bit complicated, but all it's doing is copying whatever version of node you have active via nvm into the /usr/local/ directory (where user installed global files should live on a linux VPS) and setting the permissions so that all users can access them.

> **Note**: If you ever want to change the version of node that's installed system wide, just do another nvm use vXX.XX.XX to switch your user's node to the version you want, and then re-run the above command to copy it to the system directory.

### Add symlink to set it to global:
```console
$ sudo ln -s /path/to/.nvm/current/bin/node /usr/bin/node # sudo ln -s /home/user/.nvm/current/bin/node /usr/bin/node
$ sudo ln -s /path/to/.nvm/current/bin/npm /usr/bin/npm # sudo ln -s /home/user/.nvm/current/bin/node /usr/bin/node
```

## References

- [Creationix/NVM](https://github.com/creationix/nvm)
- [DigitalOcean - How to Install Node.js with NVM](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-with-nvm-node-version-manager-on-a-vps)