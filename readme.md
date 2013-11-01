#Ubuntu Docker VirtualBox Builder
Packer.io project to build a virtualbox with docker pre-installed

##Setup
Packer.io is needed to build the image.
Installation instructions are available on the [packer.io](http://www.packer.io/intro/getting-started/setup.html) website.

##Build
Build the packer template:

```
packer build template.json
```

To test install locally:

```
vagrant box add 'box-name' ./packer_virtualbox_virtualbox.box
```

##Run

After the virtual box has been added locally it can be referenced by the 'box-name' in a Vagrantfile.

##Test

There are currently no automated tests around verifying the images. Currently testing is done by using the image on an existing project to ensure functionality still works.

##Deploy

Currently we share these virtualmachine boxes through S3 meltmedia-public-boxes (which account is this on?). Once uploaded to S3 any Vagrantfile can reference the box via the S3 url.

##How to update/re-create:

This is based on the veewee project templates available at [https://github.com/jedi4ever/veewee](https://github.com/jedi4ever/veewee)

Convert a veewee project into packer using [veewee-to-packer](http://www.packer.io/docs/templates/veewee-to-packer.html)

Select the template you want to base upon and run:

```
veewee-to-packer definition.rb
```

A docker.sh script is provided in this project. This follows the instructions on [packer.io](http://docs.docker.io/en/latest/installation/ubuntulinux/) for installation. Make sure this script is part of the scripts in the template.json

Make sure the vagrant post processor is part of the template.json. More detail is available on [packer.io](http://www.packer.io/intro/getting-started/vagrant.html)

```
"post-processors": ["vagrant"]
```

The template can be validated with

```
packer validate template.json
```

After this the build processes above can be followed.