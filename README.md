#devbox

devbox is my development environment/setup on the cloud. It is a virtual machine running Ubuntu 12.04 containing all the necessary packages installed along with it. This helps me to boot up a quick development box for myself in local/cloud when the unexpected happens.

devbox is built using [Vagrant](vagrantup.com) and [Chef-Solo](http://docs.vagrantup.com/v2/provisioning/chef_solo.html).

##Prerequisites

* Install ruby and other packages:
    ```
        curl -L https://get.rvm.io | bash -s stable --ruby
        rvm --default use 1.9.3
    ```

* Next, install Vagrant:
    ```
        gem install vagrant
    ```

* Install [Virtualbox](https://www.virtualbox.org/) (Vagrant can be configured with other [providers](http://docs.vagrantup.com/v2/getting-started/providers.html) as well.)

##Running

* Load the virtual machine using ```vagrant up```

To start using the new VM, you'll need to ssh into it using ```vagrant ssh```

Let the coding begin !
