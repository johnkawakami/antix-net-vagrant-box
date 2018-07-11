# johnk/antix-net, an AntiX box for Vagrant

I don't really know what I'm doing, so things are a little
disorganized.

This project created the johnk/antix-net Vagrant box.

However, it's not now it was bootstrapped.  That's lost
to time.

## The filename

Locally, I use:

johnk-antix-net-a.b.c.box

## Semver numbering

a.b.c

a = major release
b = minor release
    even values are releases
    odd values are alpha/betas
c = bugfix and other releases

So, after many updates to 0.0.1, I moved the 
version number to 0.1.0, an alpha number, for testing.

When "testing" is done, the version will be incremented
to 0.2.0.

## To create a new version

Mess with the box with updates, etc.

Clean out the box (docs online).

Add a line to the CHANGELOG.

Add a new version to the metafile.json.  You are specifying
the filename before it's created.

Package the box file, and put the version number in there.

    vagrant package --output johnk-antix-net-...box

Then, the box is now ready to use.

## To use the metadata to add the box to Vagrant

Next, we need to add the .box file to our local copy of Vagrant,
so we can use it for testing.

To allow us to "download" it into Vagrant with a version number,
we use the metadata.json file:

    vagrant box add /home/johnk/projects/antix-base-box/metadata.json

Fix the checksum in the metadata, and then re-run the command.

This adds the box to your local repository of boxes.

## Quick test

Make a temp directory somewhere and then:

    vagrant init johnk/antix-net

That should bring in the latest version.

    vagrant up

    vagrant ssh

It works? Good. Now exit, and wipe it out:

    vagrant halt &&  vagrant destroy
    cd ..
    rm -rf <thedirectoryyoucreated>

## In Vagrantfile

Next, test the box against all the existing code dependent on 
johnk/antix-net's previous version.  This will destroy the existing machine,
so make sure your project isn't inside the VM.  Make sure all the
project files are in a shared directory.

Go into the Vagrantfile, and change
the version:

    config.vm.box = "johnk/antix-net"
    config.vm.box_version = "0.1.0"

With your latest version.

    vagrant destroy
    vagrant up

Test that it works. Re-provisioning should take a while.

## Publish to Vagrant Cloud

Publish the box to Vagrant Cloud once it passes testing.


