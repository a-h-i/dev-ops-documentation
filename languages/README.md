# Language Support

This document details how to setup environments for various languages used currently at dreidev or those that we are planning to use / might be using in the future and consider part of our toolbelt.




## Native: C & C++

The default setup and packages include native support, check [this document](../generic/general.md).


## Python

Virtualenv per project, the deployment system for each project, which is capistrano, will setup the virtualenv for the project.

Python and python3 themselves are provided by the system and are installed as part of the default devops package on any server check [this document](../generic/general.md).


Virtualenv must be install system wide in order to be available for developers running their capistrano scripts.

To do so run `dnf install virtualenv`.


### How to create a python2 virtual env?

`virtualenv -p python2 <env-foldername>`

### How to create a python 3 virtual env?

`virtualenv -p python3 <env-foldername>`


## Node

Nvm is used to manage node version installing system node before nvm is prudent.

Simply run the install script from [nvm readme](https://github.com/creationix/nvm) 

`curl -o- https://raw.githubusercontent.com/creationix/nvm/<nvm version>/install.sh | bash`


This must be done for each user that wants node on the server.
bash must reload before there is any effect after installing nvm


`nvm install v7.7.3`
`nvm alias default v7.7.3`

Either use v7.7.1 or latest, configuration of other versions if required is done through capistrano script and `.nvmrc` file.

`nvm ls-remote` lists available versions, latest is last one printed.



## Ruby

rbenv is used to manage ruby versions, installing system ruby before rbenv is prudent.

### Rbenv installation

```bash
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
cd ~/.rbenv && src/configure && make -C src
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
```
This must be done for each user that wants ruby on the server.
bash must reload before there is any effect after installing rbenv.

List ruby versions via `rbenv install -l`

Ignore all except those of the format `2.3.1`

Install `2.3.1` or latest. `rbenv install 2.3.1`. Make the version you installed defualt `rbenv global 2.3.1`

Rehash (after installing new ruby version or gems with executables) `rbenv rehash`

Install default gems `gem install bundler pry` and rehash again.

Installing a specific version is to be handled by project maintainers via capistrano and `.ruby-version` or `RUBY_VERSION` env var.

Additional documentation [here](https://github.com/rbenv/rbenv)



