mayaviPort
==========

mayaviPort is user space daemon which exposes local server behind NAT and firewall to other mayaviPort running device or on the cloud.

* Expose localhost server to public network.
* Access raspberry pi from anywhere.
* Connect two localhost application over secure tunnel
* Get linux terminal on web console.

### Quick run

```
    ./mayaviPort -S
```

Usage
=====
```
    $ ./mayaviPort -h
    ======================================================
    mayaviPort v1.001
    Exposes TCP/HTTP server running on localhost to cloud.
    Copyright (c) SET Software Ltd. India Fri Sep 25 22:27:03 IST 2020
    ======================================================

    Usage: mayaviPort <options>
    Options:
        -f <path>    Log output to debug file instead of stdout
        -c <path>    Configuration file path
        -k <key>     Required once for registered users
        -d           Run as a daemon
        -v           Verbose log
        -i <ip>      Server ip address (optional)
        -t <port>    Local tcp app port which needs to be exposed

        -S           Start the service, show own mayavi ID
        -K           Kill the service
        -C <mayavi-ID>:<App-Port> Connect remote server with remote mayavi-ID and App-port
        -C <mayavi-Port>:<mayavi-ID>:<App-Port>
        -h help

    Terms:
        mayavi-ID:   It is unique ID like IP address which represents device where service is running.
        mayavi-Port: It is opened port in local machine or on cloud, which is tunneled to App-Port on remote machine.
        app-Port:    It is server application listener port like ssh(22), vnc

    Example:
        Usage 1): mayaviPort service should be running on both machine
        Start a service:             ./mayaviPort -S
        Connect to remote app:       ./mayaviPort -C 56805:22
    Usage 2): Expose local server on cloud. It openes remote port on cloud.
        Expose local port:           ./mayaviPort -t 1234
```

Get started
===========

### Usage 1: Expose TCP port on Cloud

TCP port will get opened on the cloud. Any client can connect to publicly available Domain/IP and port

![Screenshot](https://raw.githubusercontent.com/SunEmTech/mayaviPort/main/mayaviPort_cloud.gif)

* To expose SSH port on the cloud, execute:
```
    $ ./mayaviPort -t 22
    =================================================
    mayavi-Port online at - io.mayaviport.com : 55198
    =================================================
```
* Control the machine via SSH from any device 
```  
    $ ssh -p 55198 user@io.mayaviport.com
```
### Usage 2: Run as a service, connect to any port from remote machine.

![Screenshot](https://raw.githubusercontent.com/SunEmTech/mayaviPort/main/mayaviPort_service.gif)

* Start mayaviPort service in the machine you want to expose the services.
```
    $ ./mayaviPort -S
    =======================
    My mayaviID: 413587
    =======================

    Use this ID on remote machine to connect applications running on this machine.
    On the remote machine:
    mayaviPort -C <mayavi-ID>:<port to connect>
    example: for SSH, mayaviPort -C 413587:22
    connect via ssh: ssh -p <mayavi-Port/1807> <username>@localhost
```
* On remote machine use mayavi-ID and server application port to open local tunneled TCP port. In this example we are using SSH server to connect from remote machine.

```
    $ ./mayaviPort -C 2233:22
    ==============================
    Connect app to localhost:1807
    ==============================

    For example:
    ssh -p 1807 <username>@localhost
    or
    netcat localhost 1807
```
* Login to remote SSH via opened local port.

```
    $ ssh -p 1807 <username>@localhost
```

### Usage 3: Access device via Console

Console is a web-based terminal to access any mayaviPort running device

* Sign up and create a free account.
* Add a device.
* Copy the key and execute on device 
```
    ./mayaviPort -H <key>
```
* Start the mayaviPort application 
```
    ./ mayaviPort -S
```
* On web console, Access an added device.

### Copyright

Copyright (c) SET software systems. All right reserved.

