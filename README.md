# Server with secure lustre


## Requirements

This script assumes you have:

  *access to openstack

  *access to a secure lustre network

  *access to an image with the lustre client installed and correctly configured

  *access to a keypair in openstack

  *a server to run all this on, with the openstack CLI available.

You will additionally need:

  *your openstack credentials

  *a name to give your server

## Method of use

Source your openstack credentials and run ./createlusserv  and you will be prompted to give all the information needed.

    ./createlusserv -h
will tell you the available options (networks, secgroups, keypair, flavour, name)

The option exists to put these options into a file, for later use.  An example of such a file is provided here as var, it has place holders that you must fill in 
with valid options if you wish to use it.  The option also exists to create such a file out of your answers to prompts, should you wish to, see the help text for 
createlusserv.

This script will output the floating IP of your new server.

## Method of clean up

Source your openstack credentials and run ./deletelusserv and you will be prompted to give all the information needed.

    ./deletelusserv -h
will tell you what you can provide on the commandline.  Mainly this is the floating IP of the server you wish to delete.


## What it makes

This script makes a server (with your chosen image, flavour, and keypair); two ports, one for your regular networking with security groups and a floating IP on your 
selected network and one for secure lustre with no security groups on your selected lustre network; and attaches these things together. (The cleanup script deletes 
these things).  The mounting of the lustre is handled by the image, so you should use an image which achieves the desired state (it might mount the lustre, or leave 
it to be manually mounted).


## A note on security groups

You can provide more than one, repeat the command line option, or with a space seperated list in a file.  Or you can add security groups to the port, the script 
outputs instructions to do this.  Do not add security groups to the server, as the lustre network must have no security groups applied.
