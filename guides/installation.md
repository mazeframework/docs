---
description: That feeling you get when that right tool did all the work
---

# Installation

Maze CLI offers you a set of command line tools to **create**, **generate**, **scaffold** and **run** your projects easily and fast.

## Linux

Ensure you have the necessary dependencies:

* **Git:** Use your platform specific package manager to install `git`
* **Crystal:** Follow the instructions to get `crystal` on this page: [Crystal Installation](https://crystal-lang.org/docs/installation/index.html)
* **NodeJS and Webpack:** `node` is an optional dependency and is used to compile JavaScript and other assets.
* **PostgreSQL:** `postgres` is a relational database server. Maze configures applications to use this database adapter by default, but you can switch to MySQL by passing the flag `--database mysql` when creating a new application.

Once you have these dependencies, You can build the `maze` tool from source:

### From Source

Download and install `maze`

```bash
curl -L https://github.com/mazeframework/maze/archive/stable.tar.gz | tar xz
cd maze-stable/
make
sudo make install
```

If you run into an issue on compiling regarding `Unhandled exception in spawn: fork: Cannot allocate memory` it means you don't have enough memory. This can easily be solved by adding a swapfile.

```bash
sudo dd if=/dev/zero of=/swapfile bs=2k count=1024k
sudo mkswap /swapfile
sudo chmod 600 /swapfile
sudo swapon /swapfile
```

### For Debian & Ubuntu

* These are necessary to compile the CLI:
* `sudo apt-get install build-essential libreadline-dev libsqlite3-dev libpq-dev libmysqlclient-dev libssl-dev libyaml-dev`

### For RedHat & CentOS

* `sudo yum groupinstall development tools`
* `sudo yum install readline-devel sqlite-devel openssl-devel libyaml-devel gc-devel libevent-devel`

### For ArchLinux & derivates

* Install the CLI from [AUR package](https://aur.archlinux.org/packages/maze/). Dependencies are automatically installed.
* `yaourt -S maze`

You should now be able to run `maze` in the command line.

## Homebrew MacOS

```text
brew install maze
```

If you have previously installed maze with `brew`, you may need to uninstall and untap it:

```text
brew uninstall mazeframework/maze/maze
brew untap mazeframework/maze
```

