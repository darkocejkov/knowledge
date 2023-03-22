# Containers

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

- Containerization is *similar* to VMs, but not quite.
- Virtual Machines *emulate* hardware and software (operating system)
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

# Anatomy of a Container

## Namespaces
To fully understand containers, we need to know what *namespaces* are. They are essentially ways to emulate filesystems or "views"/"collections" of functions. For example, we can use namespaces to give "super" access to users in their local environment despite not being truly "super", or having access to root. This is because we use a namespace to emulate this functionality for that user.

| Namespace |
| --------- |
| USERNS    |
| MOUNT     |
| NET       |
| IPC       |
| PID       |
| CGROUP    |
| UTC       |

Docker is an application that abstracts containerization, and uses these namespaces to define local endpoints and their boundaries for those containers.

## Operating Systems
Technically, because containerization requires namespaces, it can only run on Linux - and some Windows (because of Linux subsystems).

# Container History
All containerization refers to, is some way to isolate programs from the filesystem. The first idea of containers comes from the `chroot()` functionality in BSD, in which you can "change root" for programs to define a root directory for them.

Technically, in terms of file-systems,  in order to containerize, or create some 'isolated environment', all you have to do it re-create the root directories in subfolders and then make programs *think* they are running in the *true root* by using that `chroot()`. 

However, a lot more stands in the way of *true* isolation, because you need some *runtime* to be running to watch each of those "isolated" environments to make sure they are allocate as much of their (needed) resources as possible.

What this requires is a lot more *process management*, and interfering with programs on the kernel level, to observe and manipulate their environments as needed.

However, this increased complexity makes it increasingly complex to create containers and manage them - as seen in the *linux containers* LXC. There are many, many steps that require manual configuration to bridge networks, manage user IDs, etc ...

That's why docker and modern containers really make sense, because they are so easy and do not require that whatsoever, or at least, to a much smaller degree.

# Virtual Environments vs. Docker
Virtual environments are very rudimentary, subsets of containers. Often, package managers and environment managers allow you to use some form of environment system, where you provide the following:
1. Name of environment
2. What's in the environment

And the "virtual" aspect works on your side to seperate these environments and switch between them easily. Sometimes it might be slightly more complex, but overall, allow you to seperate packages, libraries, and versions between environments. 
That way, when you have different projects or repositories, you can very easily switch to the appropriate environment without worrying about the overhead.
Also, think about the insane amounts of trouble it is to try and host a repository on your local machine without any form of package manager, you have to find all the dependent packages yourself in the correct versions.

## Docker Advantages
1. Docker allows you to specify *dockerfiles*, which are basically environment definitions for your project. You specify all the packages you need, environment variables, scripts, and instructions. That way, it works similar to package files that 
	1. Dockerfiles are *instructions* on how to construct the environment, which are then constructed into *images* as instances of the dockerfiles, that you can easily use to host specific services.

## Docker on non-Linux
Docker is very unique to Linux because of its control of [[#Namespaces]], to control resources between containers, and the containers "root" filesystem.

Since these namespaces are unique to Linux, then Docker is unique to Linux. Docker did something pretty smart to get itself working on non-Linux machines like macOS and windows - it used VMs as a runtime for docker to solely create containers.

Initially, Docker created `Docker Machine` using VMBox, but is now using a more modern approach with `Docker Desktop` to VMs using an apple-specific Hypervisor (Virtual Kit), and Hyper-V on Windows.

