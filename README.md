# Packer template to bake a vagrant box for virtualbox with nginx based on xenial64. A kitchen-vagrant test is included

### Prerequisites

* packer
* virtualbox
* kitchen

## Bake box

### Get the repo and bring up the environment

```
git clone https://github.com/achuchulev/packer-vagrant-nginx.git
cd packer-vagrant-nginx
```

### Validate template: 

`packer validate nginx64.json`

### Start build:

`packer build nginx64.json`

#### Please note that _packer post-processors_ will add the box automatically with following command:

`vagrant box add --name nginx64 --provider nginx64-vbox.box`

## Use box

### Confirm that the box was added:

`vagrant box list`

### Initialize vagrant:

`vagrant init -m nginx64`

### Start the box with command:

`vagrant up`

### Connect to the box with command:

`vagrant ssh`

## Test box to verify that _nginx_ is installed

### on Mac

#### Prerequisites

##### Install rbenv to use ruby version 2.3.1

```
brew install rbenv
rbenv install 2.3.1
rbenv local 2.3.1
rbenv versions
```

##### Add the following lines to your ~/.bash_profile:

```
eval "$(rbenv init -)"
true
export PATH="$HOME/.rbenv/bin:$PATH"
```

##### Reload profile: 

`source ~/.bash_profile`

##### Install bundler

```
gem install bundler
bundle install
```

#### Run the test: 

```
bundle exec kitchen list
bundle exec kitchen converge
bundle exec kitchen verify
bundle exec kitchen destroy
```

### on Linux

#### Prerequisites

```
gem install test-kitchen
gem install kitchen-inspec
gem install kitchen-vagrant
```

#### Run kitchen test 

```
kitchen list
kitchen converge
kitchen verify
kitchen destroy
```
