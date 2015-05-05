# trusty-ceph-demo
Ceph demo for Ubuntu trusty by Ansible and Vagrant.

## Abstract

This Vagrantfile will deploy the Ceph block device on Ubuntu 14.04 LTS virtual machines with VirtualBox.

## Requirements

My development environment is shown below. I think that Ubuntu LinuxBox also works.

    $ cat /etc/redhat-release
    CentOS Linux release 7.1.1503 (Core)
    $ uname -a
    Linux zouk.local 3.10.0-229.1.2.el7.x86_64 #1 SMP Fri Mar 27 03:04:26 UTC 2015 x86_64 x86_64 x86_64 GNU/Linux
    $ cat /proc/meminfo | head -6
    MemTotal:       16243556 kB
    MemFree:          153060 kB
    MemAvailable:    7363000 kB
    Buffers:            4076 kB
    Cached:          7484732 kB
    SwapCached:        15380 kB
    $ vboxmanage --version
    4.3.26r98988
    $ vagrant --version
    Vagrant 1.7.2
    $ ansible --version
    ansible 1.9.0.1
      configured module search path = None
    $ vagrant box list
    ubuntu/trusty64 (virtualbox, 0)

My Vagrant base box 'ubuntu/trusty64' obtained from the following.
https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box

## How to use

1. run `vagrant up` and `vagrant reload`
1. login to *deployer* by `vagrant ssh deployer`
1. Install the Ceph by using script like this.

    ```
    vagrant@deployer:~$ ./setup-ceph.sh
    ```

1. The following message is a successful example. Please be stopped with ctrl+c.

    ```
    [deployer][DEBUG ] write cluster configuration to /etc/ceph/{cluster}.conf
    + sudo chmod +r /etc/ceph/ceph.client.admin.keyring
    + ceph -w
        cluster 0c8178f2-f5d2-4362-b9dd-3b998e64c791
         health HEALTH_WARN 192 pgs stuck inactive; 192 pgs stuck unclean
         monmap e1: 3 mons at {sv1=10.0.0.51:6789/0,sv2=10.0.0.52:6789/0,sv3=10.0.0.53:6789/0}, election epoch 6, quorum 0,1,2 sv1,sv2,sv3
         osdmap e5: 3 osds: 2 up, 2 in
          pgmap v6: 192 pgs, 3 pools, 0 bytes data, 0 objects
                0 kB used, 0 kB / 0 kB avail
                     192 creating

    2015-05-05 13:19:44.747004 mon.0 [INF] pgmap v5: 192 pgs: 192 creating; 0 bytes data, 0 kB used, 0 kB / 0 kB avail
    2015-05-05 13:19:45.748987 mon.0 [INF] osd.1 10.0.0.52:6800/7246 boot
    2015-05-05 13:19:45.749507 mon.0 [INF] osdmap e5: 3 osds: 2 up, 2 in
    ```

1. My Ceph version is show below.(see https://ceph.com/docs/v0.80/ )

    ```
    vagrant@deployer:~$ ceph --version
    ceph version 0.80.9 (b5a67f0e1d15385bc0d60a6da6e7fc810bde6047)
    ```

## Restrictions

1. ceph-mds is not installed.

## Memo

1. If you run `./setup-ceph.sh` twice, the all previous Ceph data are discarded.
