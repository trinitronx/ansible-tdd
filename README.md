Ansible TDD Research
====================

This repo contains some submodule repos & resources for Ansible TDD, BDD, XDD, and such.
It includes many examples given and sourced from these sources:

 - [Tighten Your Quality Feedback Loop][1]
 - [Infrastructure Testing with Ansible and Serverspec][2]
 - [kitchen-ansible Test Kitchen Provisioner][4]

Installing TDD Tools
====================

 1. Install [ChefDK][3] (Current version: 0.2.0)
   - [Mac][chefdk-mac]
   - [Ubuntu][chefdk-ubuntu]
   - [Windows][chefdk-win]
 2. Install [kitchen-ansible gem][4]<br/>`$(/opt/chefdk/bin/chef shell-init $(basename $SHELL)); sudo /opt/chefdk/embedded/bin/gem install kitchen-ansible --version 0.0.1`
 3. Install [VirtualBox][6] (Current version: 4.3.14 r95030)
   - [Mac][vbox-mac]
   - [Linux][vbox-lin]
   - [Ubuntu][vbox-ubuntu]
   - [Windows][vbox-win]
 4. Install [Vagrant][7] (Current version: 1.6.3)
   - [Mac][vagrant-mac]
   - [Ubuntu][vagrant-ubuntu]
   - [Windows][vagrant-win]

Now you're ready to use test-kitchen along with the [`kitchen-ansible`][4] Provisioner.

Running Test Kitchen & Serverspec Example
=========================================

The ansible-examples repo contains a demo of using [`test-kitchen`][5] with ansible and the [`kitchen-ansible`][4] Provisioner.  To try it out:

 1. Checkout submodule repos: `git submodule init`
 2. `cd ansible-examples/tomcat-standalone`
 3. Run Test Kitchen: `kitchen test`

[1]: https://mestachs.wordpress.com/tag/server-spec/
[2]: http://sharknet.us/2014/02/06/infrastructure-testing-with-ansible-and-serverspec-part-2/
[3]: http://downloads.getchef.com/chef-dk/
[4]: https://github.com/neillturner/kitchen-ansible
[5]: http://kitchen.ci
[6]: https://www.virtualbox.org/
[7]: http://www.vagrantup.com/downloads.html

[chefdk-mac]: https://opscode-omnibus-packages.s3.amazonaws.com/mac_os_x/10.9/x86_64/chefdk-0.2.0-2.dmg
[chefdk-ubuntu]: https://opscode-omnibus-packages.s3.amazonaws.com/ubuntu/12.04/x86_64/chefdk_0.2.0-2_amd64.deb
[chefdk-win]: https://opscode-omnibus-packages.s3.amazonaws.com/windows/2008r2/x86_64/chefdk-windows-0.2.0-2.windows.msi
[vbox-mac]: http://download.virtualbox.org/virtualbox/4.3.14/VirtualBox-4.3.14-95030-OSX.dmg
[vbox-win]: http://download.virtualbox.org/virtualbox/4.3.14/VirtualBox-4.3.14-95030-Win.exe
[vbox-lin]: https://www.virtualbox.org/wiki/Linux_Downloads
[vbox-ubuntu]: http://download.virtualbox.org/virtualbox/4.3.14/virtualbox-4.3_4.3.14-95030~Ubuntu~precise_amd64.deb
[vagrant-mac]: https://dl.bintray.com/mitchellh/vagrant/vagrant_1.6.3.dmg
[vagrant-ubuntu]: https://dl.bintray.com/mitchellh/vagrant/vagrant_1.6.3_x86_64.deb
[vagrant-win]: https://dl.bintray.com/mitchellh/vagrant/vagrant_1.6.3.msi
