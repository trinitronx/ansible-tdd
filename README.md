Ansible TDD Research
====================

This repo contains some submodule repos & resources for Ansible TDD, BDD, XDD, and such.
It includes many examples given and sourced from these sources:

 - [Tighten Your Quality Feedback Loop][1]
 - [Infrastructure Testing with Ansible and Serverspec][2]
 - [kitchen-ansible Test Kitchen Provisioner][4]

If you are not familiar with [Test Kitchen][5], I suggest you view the quick [test-kitchen demo slideshow here][8].
If you have more time, you might want to also check out Fletcher Nichol's full [DevOps Days Presentation here][9].

Installing TDD Tools
====================

 1. Install [ChefDK][3] (Current version: 0.10.0)
   - [Mac][chefdk-mac]
   - [Ubuntu][chefdk-ubuntu]
   - [Windows][chefdk-win]
 2. Install [kitchen-ansible gem][4]<br/>`$(/opt/chefdk/bin/chef shell-init $(basename $SHELL)); sudo /opt/chefdk/embedded/bin/gem install kitchen-ansible`<br/>OR install to `~/.chefdk/gems/` (with ChefDK >= 0.3.1):<br/>`chef gem install kitchen-ansible`
 3. Install [VirtualBox][6] (Current version: 4.3.28)
   - [Mac][vbox-mac]  (Install via `.dmg` or via [brew-cask][homebrew-cask]: `brew cask install virtualbox`)
   - [Linux][vbox-lin]
   - [Ubuntu x86_64 (14.04 Trusty LTS, 14.10 Utopic, 15.04 Vivid)][vbox-ubuntu]
   - [Windows][vbox-win]
 4. Install [Vagrant][7] (Current version: 1.7.2)
   - [Mac][vagrant-mac]  (Install via `.dmg` or via [brew-cask][homebrew-cask]: `brew cask install vagrant`)
   - [Ubuntu][vagrant-ubuntu]
   - [Windows][vagrant-win]

Now you're ready to use test-kitchen along with the [`kitchen-ansible`][4] Provisioner.

Running Test Kitchen & Serverspec Example
=========================================

The ansible-examples repo contains a demo of using [`test-kitchen`][5] with ansible and the [`kitchen-ansible`][4] Provisioner.  To try it out:

 1. Checkout submodule repos: `git submodule update --init`
 2. `cd ansible-examples/tomcat-standalone`
 3. Run Test Kitchen: `kitchen test`

[1]: https://mestachs.wordpress.com/tag/server-spec/
[2]: http://sharknet.us/2014/02/06/infrastructure-testing-with-ansible-and-serverspec-part-2/
[3]: http://downloads.getchef.com/chef-dk/
[4]: https://github.com/neillturner/kitchen-ansible
[5]: http://kitchen.ci
[6]: https://www.virtualbox.org/
[7]: http://www.vagrantup.com/downloads.html
[8]: http://www.slideshare.net/tomduffield/test-kitchen-demo
[9]: http://www.slideshare.net/devopsdays/test-kitchen-10-fletcher-nichol

[chefdk-mac]: https://downloads.chef.io/chef-dk/mac/
[chefdk-ubuntu]: https://downloads.chef.io/chef-dk/ubuntu/
[chefdk-win]: https://downloads.chef.io/chef-dk/windows/
[vbox-mac]: http://download.virtualbox.org/virtualbox/5.0.10/VirtualBox-5.0.10-104061-OSX.dmg
[vbox-win]: http://download.virtualbox.org/virtualbox/5.0.10/VirtualBox-5.0.10-104061-Win.exe
[vbox-lin]: https://www.virtualbox.org/wiki/Linux_Downloads
[vbox-ubuntu]: http://download.virtualbox.org/virtualbox/5.0.10/virtualbox-5.0_5.0.10-104061~Ubuntu~trusty_amd64.deb
[vagrant-mac]: https://dl.bintray.com/mitchellh/vagrant/vagrant_1.7.4.dmg
[vagrant-ubuntu]: https://dl.bintray.com/mitchellh/vagrant/vagrant_1.7.4_x86_64.deb
[vagrant-win]: https://dl.bintray.com/mitchellh/vagrant/vagrant_1.7.4.msi
[homebrew-cask]: http://caskroom.io/
