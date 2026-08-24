# Server Information

## Server Overview

  Item               Value
  ------------------ --------------------------------------
  Server Role        Deployment Target Server
  Operating System   Ubuntu 22.04.5 LTS (Jammy Jellyfish)
  Hostname           target
  IP Address         172.20.10.5

------------------------------------------------------------------------

## Access Information

  Item                    Value
  ----------------------- ---------------
  SSH Method              SSH
  SSH Port                22
  Username                ubuntu
  Authentication Method   Not specified

------------------------------------------------------------------------

## System Specifications

## CPU

  Item                  Value
  --------------------- ------------------------------------------
  Architecture          x86_64
  CPU Model             Intel(R) Xeon(R) CPU E5-2680 0 @ 2.70GHz
  CPU Count             4 vCPU
  CPU Cores             4
  CPU Sockets           1
  Hypervisor            VMware
  Virtualization Type   Full Virtualization

------------------------------------------------------------------------

## Memory

  Item            Value
  --------------- ---------
  Total RAM       3.8 GiB
  Available RAM   3.4 GiB
  Swap            4.0 GiB

------------------------------------------------------------------------

## Storage

  Item              Value
  ----------------- ---------------------------
  Disk              /dev/sda
  Total Disk Size   100G
  Root Partition    86.9G LVM
  Root Usage        7.5G used / 74G available
  /tmp Partition    10G LVM

------------------------------------------------------------------------

## Network Information

  Item                Value
  ------------------- -------------------
  Network Interface   ens33
  IP Address          172.20.10.5/24
  MAC Address         00:50:56:a7:75:79

------------------------------------------------------------------------

## Operating System Details

  Item             Value
  ---------------- --------------------
  Distribution     Ubuntu
  Version          22.04.5 LTS
  Codename         jammy
  Kernel Version   5.15.0-187-generic

------------------------------------------------------------------------

## Deployment Notes

-   This server is the target environment for the Docker and Ansible
    deployment project.
-   Server preparation will be automated using Ansible.
-   Application services will be deployed using Docker and Docker
    Compose.
-   Nginx will run as a Docker container and act as Reverse Proxy.
