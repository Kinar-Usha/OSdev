# My first try writing a 64-bit Operating System Kernel

## Prerequisites
 - [VS Code](https://code.visualstudio.com/).
 - [Docker](https://www.docker.com/) for creating our build-environment.
 - [Qemu](https://www.qemu.org/) for emulating our operating system.
 
 ## Setup
 Build an image for our env:
  - `docker build buildenv -t myos-buildenv`
  
## Build

Enter build env:
-`docker run --rm -it -v "$pwd":/root/env myos-buildenv`

Build for x86:
- `make build-x86_64`

To leave the build environment, enter `exit`.

##Emulate
- `qemu-system-x86_64 -cdrom dist/x86_64/kernel.iso`
Alternatively, you should be able to load the operating system on a USB drive and boot into it when you turn on your computer. (I haven't actually tested this yet.)

## Cleanup

Remove the build-evironment image:
 - `docker rmi myos-buildenv -f`
 
Mistakes I made
 - I am using a Windows 10 Home so Docker for desktop(hyper-v) doesnt work so use the docker for desktop with instegrated with wsl
 VS code has a remote -wsl feature.
 
 - While in the build env, if ran `make build-x86_64`, `No rule to make target 'build-x86_64`,
 my wsl wouldnt recognise the files in the directory (if you `ls` no files would be shown).
 solution-
    export pwd=/path/of/repo/root
    sudo docker run --rm -it -v "$(pwd)":/root/env myos-buildenv
    then agian run your docker image
    
