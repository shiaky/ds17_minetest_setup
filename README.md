# ds17_minetest_setup

## What do you need?
* hypervisor computer
* plastic WiFi router or other private network


## Setup
1. install `vagrant` and `virtualbox`
2. clone the repo
3. change to directory of the repo
4. run `vagrant up`
5. choose a network device to which the VM will be bridged
  * the VM has a special MAC address (`08:00:27:ff:ff:ff`) to give you the opportunity to set a static IP address for the VM in your network
6. in the output you will see the status of the minetest server service and the current IP address of your bridged VM network device
7. connect a bunch of computers having minetest >4.16 installed to the plastic WiFi router or the internal network
8. go to the `play-online` tab and choose your VM IP address as the server
  * if you have a local DNS Server propagating the hostnames, you can reach the server via minetest.localdomain

Default admin user: *snoop*

Make sure to be the first person joining the server having the username *snoop*. Dont forget to set a password.
