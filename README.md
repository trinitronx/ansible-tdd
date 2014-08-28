Ansible TDD Research
====================

This repo contains some submodule repos & resources for Ansible TDD, BDD, XDD, and such.
It includes many examples given and sourced from these sources:

 - [Tighten Your Quality Feedback Loop][1]
 - [Infrastructure Testing with Ansible and Serverspec][2]
 - [kitchen-ansible Test Kitchen Provisioner][4]

Installing TDD Tools
====================

 1. Install [ChefDK][3] (Current version: 0.2.0 - [Mac][chefdk-mac] [Ubuntu][chefdk-ubuntu] [Windows][chefdk-win])
 2. Install [kitchen-ansible gem][4]<br/>`$(/opt/chefdk/bin/chef shell-init $(basename $SHELL)); sudo /opt/chefdk/embedded/bin/gem install kitchen-ansible --version 0.0.1`

Now you're ready to use test-kitchen along with the [`kitchen-ansible`][4] Provisioner.

[1]: https://mestachs.wordpress.com/tag/server-spec/
[2]: http://sharknet.us/2014/02/06/infrastructure-testing-with-ansible-and-serverspec-part-2/
[3]: http://downloads.getchef.com/chef-dk/
[4]: https://github.com/neillturner/kitchen-ansible

[chefdk-mac]: https://opscode-omnibus-packages.s3.amazonaws.com/mac_os_x/10.9/x86_64/chefdk-0.2.0-2.dmg
[chefdk-ubuntu]: https://opscode-omnibus-packages.s3.amazonaws.com/ubuntu/12.04/x86_64/chefdk_0.2.0-2_amd64.deb
[chefdk-win]: https://opscode-omnibus-packages.s3.amazonaws.com/windows/2008r2/x86_64/chefdk-windows-0.2.0-2.windows.msi
