# Setup a Full Shellpay Node

These instructions are based on Linux Ubuntu 14.04, any other Unix based distribution should work quite similar.

As `root` run the following commands:


```
# Install Docker
wget -qO- https://get.docker.com/ | sh

# Install Fig, see for latest version: http://www.fig.sh/install.html
curl -L https://github.com/docker/fig/releases/download/1.0.1/fig-`uname -s`-`uname -m` > /usr/local/bin/fig
chmod +x /usr/local/bin/fig

# Clone all the necessary repos into a project folder:
cd
git clone https://github.com/Shellpay/dpnode.git
cd dpnode
git clone https://github.com/Shellpay/ShellCoind-docker.git
git clone https://github.com/Shellpay/insight-docker.git
git clone https://github.com/Shellpay/insight-shell-api.git
git clone https://github.com/Shellpay/shellpartyd-docker.git
git clone https://github.com/Shellpay/shellblockd-docker.git
git clone https://github.com/Shellpay/shellparty-wallet-dev-server-docker.git

# Link the Dockerfile for the insight.js project to build a container with it later
ln insight-docker/Dockerfile insight-shell-api/Dockerfile

# Let's build all machines
fig build

# start the beast
# CTRL-C then stops only the log tail, not the components
fig up -d ; fig logs

# check the status of each node with:
# (each component should have the status 'up'
fig ps

# Usually shellpartyd doesn't have enought time to start, restart with:
fig scale shellpartyd=1
```

