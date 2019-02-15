VM of development LIV LYON
===================

Prerequisites
----------

- Installation of Git GUI (https://git-scm.com/download/gui/windows)
- Virtualbox (https://www.virtualbox.org/wiki/Downloads) Version 5.1.14
- vagrant (https://www.vagrantup.com/downloads.html) Version 1.9.0
- vagrant vbguest plugin (since Git BASH: "vagrant plugin install vagrant-vbguest")
- vagrant proxyconf plugin if proxy present (from Git BASH: "vagrant plugin install vagrant-proxyconf")

For users under windows behind a proxy it is necessary to register the proxy and include the plugin-source directive.

In git bash:

```
$ export http_proxy=http://<user>:<pass>@<proxy>:<port>
$ export https_proxy=http://<user>:<pass>@<proxy>:<port>
$ vagrant plugin install plugin vagrant-vbguest --plugin-source http://rubygems.org
```

Proxy management
----------
- If you are behind a proxy:
In the.vagrant.d folder of your personal folder (C:/Users/*******/.vagrant.d/) Make sure you have a Vagrantfile with the proxy configured:

```
#C:/Users/*********/.vagrant.d/Vagrantfile

Vagrant.configure("2") do |config|
  if Vagrant.has_plugin?
    enable_proxies = true
    config.proxy.http = "http://<user>:<pass>@<proxy>:<port>"
    config.proxy.https = "http://<user>:<pass>@<proxy>:<port>"
    config.proxy.no_proxy = "localhost,127.0.0.0.1,.example.com"
  end
  if Vagrant.has_plugin?
    #config.vbguest.auto_update = true
  end
end
```

Preparation of the settings file
----------

From the directory dev Copy the file example.settings.yml to settings.yml

```
$ cp example.settings.yml settings.yml settings.yml
```

In the settings.yml file,

 *  fill in the path to the provisioning of the ibon Validite unique project (root of the provisioning repository to be cloned from Stash/Git)

provison: host_path: <path_to_provisionning>''

Branch of each directory to be used:
------------
- dev: develop
- provisionning: develop

```
#.../dev
	$ git checkout develop

#.../provisionning
	$ git checkout develop
```


Start the VM
------------

From the dev directory and preferably with Git BASH Start VM (in administrator mode under windows)

```
$ vagrant up
```

To connect to the VM
------------

```
$ ssh vagrant
```
the sources are in the directory /vagrant/sources
