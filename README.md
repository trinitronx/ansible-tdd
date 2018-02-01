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
 2. Install [kitchen-ansible gem][4]
   - If you have `rvm` installed, first: `rvm use system`
   - With ChefDK < 0.3.1:
     - install to `/opt/chefdk/embedded/lib/ruby/gems/2.1.0/gems/` with: `$(/opt/chefdk/bin/chef shell-init $(basename $SHELL)); sudo /opt/chefdk/embedded/bin/gem install kitchen-ansible`
   - *OR* With ChefDK >= 0.3.1:
     - Install to `~/.chefdk/gem/ruby/2.1.0/gems/` with: `chef exec gem install kitchen-ansible`  (**Recommended**)
     - Install to `/opt/chefdk/embedded/lib/ruby/gems/2.1.0/gems/` with: `sudo chef gem install kitchen-ansible`  (**NOTE**: This will install to system ChefDK location!)
 3. Install [VirtualBox][6] (Current version: 5.0.10)
   - [Mac][vbox-mac]  (Install via `.dmg` or via [brew-cask][homebrew-cask]: `brew cask install virtualbox`)
   - [Linux][vbox-lin]
   - [Ubuntu x86_64 (14.04 Trusty LTS, 14.10 Utopic, 15.04 Vivid)][vbox-ubuntu]
   - [Windows][vbox-win]
 4. Install [Vagrant][7] (Current version: 1.7.4)
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

Ansible Guard Syntax Check Example
==================================

When developing playbooks and roles, it's helpful to have YAML syntax check (and of course `ansible-playbook --syntax-check`).  In this repo is an example `Guardfile` for using the [Guard Ruby gem][guard-gem] to do this automatically for you each time you edit a file!  Plus, it notifies you of results via a "growl" style notification (on Mac).  This should also work on Windows or Linux with the alternate gems listed in `Gemfile`, but this has not been tested for a while!.

To use this example, you first need Ruby >= 2.3 or >= 2.2.6.  I used Ruby 2.2.5 via [RVM][rvm].  You also need to install [`bundler`][bundler] (`gem install bundler`).

Once you have Ruby and `bundler`, all you need is:

```
# Make sure you are in this repo's directory!
# cd path/to/ansible-tdd/
bundle install
bundle exec guard
```

Now, try editing a file to introduce a syntax error and Guard will notify you! (It also shows if syntax check result was success)

If you are using playbooks with Ansible Vault vars files, you need to place your Vault password files (just a text file containing the Ansible Vault encryption password) into `$HOME/secrets/`.

This example `Guardfile` has this path hardcoded, and uses a naming convention based on the playbook name!  If you want to modify this location, edit your `Guardfile` appropriately.

For a playbook with encrypted vars file, use task: `- include_vars: path/to/your/encrypted-vars.yml`

If the playbook directory was named `foo-playbook`, place the Ansible Vault password file in this location:  `$HOME/secrets/ansible-vault-foo-playbook`

The reason this is necessary is because `ansible-playbook --syntax-check` will throw an error if the playbook cannot decrypt the Ansible vault vars file, and also if you try to use an undefined variable. To work around this, the example `Guardfile` checks for existence of a Vault password file in `~/secrets` that matches the playbook name.  If found, it passes this in to `ansible-playbook --syntax-check` via  `--vault-password-file=$HOME/secrets/ansible-vault-<PLAYBOOK_NAME>`.



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

[guard-gem]: http://guardgem.org/
[bundler]: http://bundler.io/
[rvm]: https://rvm.io/
