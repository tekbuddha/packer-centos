These [packer](http://packer.io) templates are used to build "latest and greatest" [vagrant](http://vagrantup.com) boxes. It is derived from work I did originally while working at [New Context](https://github.com/newcontext/packer-centos). The templates will build boxes for both VirtualBox and VMware Fusion, installing the latest set of vmtools respectively. They are to generate both minimal-OS (base) boxes in addition to boxes with Chef pre-installed. These templates have also been expanded to include support for generating images for AWS and Digital Ocean.

## How do I use this?

If you want to build these boxes, packer is very easy to use. First, install [packer](http://packer.io). On a Mac, it's easiest to install it via [Homebrew](http://brew.sh):

	$ brew install homebrew/binary/packer


Verify it installed properly:

	$ packer -v
	Packer v0.4.1


You'll obviously need a copy of this repository:

	$ git clone https://github.com/newcontext/packer-centos


Creation of base boxes is as straightforward as:

	$ packer build templates/centos64.json


This will build CentOS 6.4 base boxes for both Virtualbox and VMware. How about building only for virtualbox, you ask?:

	$ packer build -only=virtualbox templates/centos64.json


Building boxes with the latest Chef?:

	$ packer build -var "provisioner=chef" -var "provisioner_version=latest" templates/centos64.json


What if that last run fails to build a VMware box properly?:

	$ packer build -var "provisioner=chef" -var "provisioner_version=latest" -only=vmware templates/centos64.json


Need an older version of Chef installed?:

	$ packer build -var "provisioner=chef" -var "provisioner_version=11.6.2" templates/centos64.json

*IMPORTANT*: The version specified must still be avialable for download from the Chef website.


In all build scenarios, successfully packed boxes will be stored in _boxes/virtualbox/_ or _boxes/vmware/_.
