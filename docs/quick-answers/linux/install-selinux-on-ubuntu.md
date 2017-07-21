---
author:
  name: Angel
  email: docs@linode.com
description: 'This Quick Answer guide shows you how to install SELinux on Ubuntu after you've uninstalled apparmor'
keywords: 'linux,selinux,apparmor,Mandatory Access Control system'
license: '[CC BY-ND 4.0](https://creativecommons.org/licenses/by-nd/4.0)'
modified: 'Sunday, June 30th, 2017'
modified_by:
  name: Angel Guarisma
published: 'Sunday, June 30th, 2017'
title: How to Install SELinux on Ubuntu
---


### Install SELinux on Ubuntu

Ubuntu has a Mandatory Access Control (MAC) system similar to SELinux, named AppArmor. Both SELinux and AppArmor provide a set of tools to isolate applications from each other to protect the host system from being compromised. AppArmor offers Ubuntu users mandatory access control options, without the perceived difficulty or learning curve that SELinux may have. However, if you are switching to Ubuntu, are already familiar with SELinux and would like to use it to enforce security on your system, you can install it by following this brief tutorial. 

#### Before You Begin

Linode does not support SELinux by default. To boot a distribution-specific kernel, follow this [guide](https://www.linode.com/docs/tools-reference/custom-kernels-distros/run-a-distribution-supplied-kernel-with-kvm), and select GRUB2 in the manager's kernel menu. 

#### Remove AppArmor

{:.caution}
>
>At this point in the tutorial AppArmor is your default security module. Removing but not replacing AppArmor can put your system at risk.
>Do not purge AppArmor if you believe you may reuse it in the future. 

1. Stop the AppArmor script in `/etc/init.d/`: 

		sudo /etc/init.d/apparmor stop 

2. Purge AppArmor from the system. 
	
		apt purge apparmor

	If you are worried about configuration files being removed from the system, use `apt remove apparmor`. 

3. Update and reboot your system: 

		apt update && upgrade -yuf
		reboot

#### Install SELinux

1. Install the SELinux package and reboot the system:

		apt install selinux
		reboot

2. You can determine whether or not SELinux is enforcing security on your system by trying to set SELinux to `enforcing` mode. 

		root@ubuntu:~# setenforce 1
		root@ubuntu:~# getenforce
		Enforcing

{:.note}
>
>If you receive the error message, `setenforce: SELinux is disabled`, check if you are still using the Linode custom kernel. If so, disable the custom kernel and try installing SELinux again.

## Next Steps 
After installing SELinux on your system, use our [Getting Started with SELinux Guide](/docs/security/getting-started-with-selinux) to learn the basics of SELinux security. 