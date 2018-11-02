# Packer template to bake a vagrant box for virtualbox with nginx based on xenial64. A kitchen-vagrant test is included

### Prerequisites

* packer
* virtualbox
* kitchen

## Bake box

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

## Test box

### Run kitchen test to verify that _nginx_ is installed with following commands:

```
kitchen list
kitchen converge
kitchen verify
kitchen destroy
```
