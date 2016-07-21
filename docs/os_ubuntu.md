### Apps

**IntellIJ**

```

```

#### Install git

```shell
apt-get install -y git
```

### GUI `ubuntu-desktop

```
apt-get install ubuntu-desktop
```

Then restart computer, ubuntu-desktop will run in the next login.

# Install IntellIJ in ubuntu


###  Downloads intellij
```
https://www.jetbrains.com/idea/download/
```


### Create Ubuntu desktop launcher

run intellij : cd to folder intellij
```
cd file://path intellij/idea.sh
```

  Create Ubuntu desktop
```
Tools > Create Desktop Entry
```

# Install Pycharm on Ubuntu

Step 1. To add the PPA, open terminal from the Dash, Launcher, or via Ctrl+Alt+T shortcut keys. When it opens, run command:

```
sudo add-apt-repository ppa:mystic-mirage/pycharm
```

Step 2. After adding the PPA, update system package cache and install the IDE via Synaptic Package Manager. Or just run below commands one by one in terminal:

```
sudo apt-get update

sudo apt-get install pycharm
```

Step 3. After finishing the installation, start Pycharm. It will prompt you to activate with license, choose the `License Server` checkbox and copy below row to it:

```
http://idea.qinxi1992.cn
```
