# kubeadmx

- update 10/29/2021 : BP support both CentOS7 and Ubuntu.
  CentOS7 image from http://download.nutanix.com/Calm/CentOS-7-x86_64-1908.qcow2
  Ubuntu image from 
    https://cloud-images.ubuntu.com/releases/focal/release/ubuntu-20.04-server-cloudimg-amd64.img
    https://cloud-images.ubuntu.com/releases/bionic/release/ubuntu-18.04-server-cloudimg-amd64.img

  Both use cloud-init:
#cloud-config
repo_update: true
repo_upgrade: all
package_upgrade: true
disable_root: False
ssh_enabled: True
chpasswd: { expire: False }
users:
- name: nutanix
  sudo: ALL=(ALL) NOPASSWD:ALL
  groups: wheel, users
  lock_passwd: false
  plain_text_passwd: nutanix/4u
  shell: /bin/bash
  ssh_authorized_keys:
    - ssh-rsa AAA.....(insert your ssh key here) nutanix
packages:
 - git
 - curl
 - htop
 - wget
final_message: "The system is finally up, after $UPTIME seconds"

  To increase qcow2 root volume size, upload the image from the link provided aboved and then create a VM with a disk from that image.  Do not need to start VM.  Add a new Disk Image with the vdisk from the just created VM and adjust the size as desired.  Now, use this new disk in the Blueprint.

Calm blue print that uses kubeadm to create k8s cluster. 
- Calico

