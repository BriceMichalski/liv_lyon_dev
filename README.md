VM de dev LIV LYON
===================

Prérequis
----------

- Installation de Git GUI : https://wikidigital.fr.carrefour.com/pages/viewpageattachments.action?pageId=5768215&metadataLink=true
- Virtualbox (https://www.virtualbox.org/wiki/Downloads) Version 5.1.14
- vagrant (https://www.vagrantup.com/downloads.html) Version 1.9.0
- vagrant vbguest plugin (depuis Git BASH : "vagrant plugin install vagrant-vbguest")
- vagrant proxyconf plugin si proxy présent (depuis Git BASH : "vagrant plugin install vagrant-proxyconf")

Pour les utilisateurs sous windows derrière un proxy il est nécessaire d'enregistrer le proxy et d'inclure la directive plugin-source.

Dans git bash:

```
$ export http_proxy=http://<user>:<pass>@<proxy>:<port>
$ export https_proxy=http://<user>:<pass>@<proxy>:<port>
$ vagrant plugin install vagrant-vbguest --plugin-source http://rubygems.org
```

Gestion du proxy
----------
- Si vous êtes derrière un proxy:

Dans le dossier .vagrant.d de votre dossier personnel (C:/Utilisateurs/FR*****/.vagrant.d/)
Assurez-vous d'avoir un Vagrantfile avec le proxy de configuré:

```
#C:/Utilisateurs/FR*****/.vagrant.d/Vagrantfile

Vagrant.configure("2") do |config|
  if Vagrant.has_plugin?("vagrant-proxyconf")
    enable_proxies = true
    config.proxy.http     = "http://<user>:<pass>@<proxy>:<port>"
    config.proxy.https    = "http://<user>:<pass>@<proxy>:<port>"
    config.proxy.no_proxy = "localhost,127.0.0.1,.example.com"
  end
  if Vagrant.has_plugin?("vagrant-vbguest")
    #config.vbguest.auto_update = true
  end
end
```



Préparation du fichier settings
----------

Depuis le répertoire dev
Copier le fichier example.settings.yml en settings.yml

```
$ cp example.settings.yml settings.yml
```
Dans le fichier settings.yml,

 * renseigner le chemin vers le provisionning du projet ibon Validite unique (racine du dépôt provisionning à cloner depuis Stash/Git)
 
	provison:
  		host_path: '<path_to_provisionning>'

Branche de chaque répertoire à utiliser :
------------

- dev: develop
- provisionning: develop

```
#../dev
	$ git checkout develop

#../provisionning
	$ git checkout develop
```

Lancer la VM
------------

Depuis le répertoire dev et de préférence avec Git BASH
Démarrer la VM (en mode administrateur sous windows)

```
$ vagrant up
```

Pour se connecter à la VM
------------

```
$ vagrant ssh
```

les sources se trouve dans le repertoire /vagrant/sources
