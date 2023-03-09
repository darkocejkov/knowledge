# Docker

## What is Docker?

- Docker is software that allows you to use ********************************containerization******************************** of images to run code in repeatable environments
- why would

## Docker use-case

<aside>
⭐ Perhaps we create an app on our machine that does a set of functions and fulfills some goal. Once we finish developing this app, whether it’s native or web, in order to get people to use it and distribute it, we need to share it.

- Especially for web applications, this process can be very difficult, because suddenly when many different users start using your app it does not work the way it’s intended to.
    - This is due to the differences in environment the app runs in, because not everyone who runs your app may have the correct tools or software pre-installed to get it to work.

Thus, we can utilise Docker and it’s containerization of images to solve this, because in order to run your app, people use Docker to run an image of a container, which contains your app.

- The core difference is that when they do so, the docker image and container is able to know/understand/pre-install dependencies within the container
    - the App that runs in the image, has access to all these dependencies and everyone who then uses this Docker image will have the EXACT environment for it to work correctly, while being silo-ed away from the parent machine
</aside>

## Containers vs. Virtual Machines

Why go through all this trouble to containerize when Virtual Machines (VMs) exist? you can just create VMs with exact OS and Hardware specs.

- because Containerization is ********similar******** to VMs, but not quite.
- Virtual Machines **************emulate************** hardware and software (operating system)
    - hypervisor emulates real hardware using existing hardware, and bridge the VMs to the host machine
    - VMs require installation and configuration of the OS
    - VMs can run multiple apps at once, but cannot interact with the hosts (which is what makes them secure)
    - require significantly more disk/hardware space, as those virtual disks need to exist somehow in the physical
- Containers however, do not emulate hardware, because they are just localized operating system environments that run SINGLE apps
    - containers run using a container “runtime” (which is what Docker is)
    - the OS of the containers are identical to the host machine
        - do not have to start up and are very quick, no OS configuration
    - can interact with hosts

![Untitled](Docker,%20Kubernetes%2074f8bde9e59e4674bc36acec0dd855ec/Untitled.png)