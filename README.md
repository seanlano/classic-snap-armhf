# Classic dimension for snappy (on armhf)

This snap allows to run a "classic" ubuntu environment on a Snappy
system. This means that the traditional package management tools like
apt and dpkg are available in this environment. It also means that
tools like `gdb`, `tcpdump`, `strace` and `valgrind` (to name a few)
are just a simple `apt install strace` away.

**NOTE:** This is a fork of the "proper" [classic-snap](https://github.com/snapcore/classic-snap) repo, modified to target `armhf` on Ubuntu Core 18. I haven't pushed this snap package up to the Snap Store, you will need to build it locally.

## Building

You will need `snapcraft` and [`multipass`](https://discourse.ubuntu.com/t/beta-release-multipass/2696) installed. 

Then clone this repo, and run Snapcraft:

```
snapcraft --target-arch=armhf
```

This should produce a file something like `classic-armhf_core18-1_armhf.snap`

## Installing

Copy the built Snap file to your target, via SCP or some other method. 

Install it and set up the slot connections with:

```
sudo snap install --dangerous --devmode classic-armhf_core18-1_armhf.snap 
sudo snap connect classic-armhf:classic-support :classic-support
```

## How to use it

Enter the classic environment with:

```
$ sudo classic-armhf
...
(classic)ubuntu@localhost:~$ sudo apt update
(classic)ubuntu@localhost:~$ exit
$
```

The environment is very lightweight and full hardware and network
access is possible.

**NOTE:** I have not done much testing with this `armhf` version, it seems to work for me in simple tests but it may break in various other ways. 

## Restrictions

Daemons are not started in the classic dimension and all running
background binaries will exit when the classic dimension is closed.
