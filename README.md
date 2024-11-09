# Wordpess-chart
## Description
Helm chart includes wordpress and mysql database.

## Prerequsites
* `Kubernetes` cluster
* `Helm` installed

## Installation
1. Clone this repo with `git clone`.
1. Edit [values.yaml](./values.yaml). Variables are self-described.
1. Install chart
    ```bash
    helm install wordpress wordpress-chart -f wordpress-chart/values.yaml --create-namespace -n wordpress
    ```
1. Get worpress address and port. Commands will be present after chart installation. Example:
    ```bash
    export NODE_PORT=$(kubectl get --namespace wordpress -o jsonpath="{.spec.ports[0].nodePort}" services wordpress-wordpress)
    export NODE_IP=$(kubectl get nodes --namespace wordpress -o jsonpath="{.items[0].status.addresses[0].address}")
    echo http://$NODE_IP:$NODE_PORT
    ```
1. Set up proxy to node port to get access.

## Github Actions
1. Create following repository actions secrets:
    * `BASTION_IP` - IP address of control-plane or bastion host with ssh access
    * `AMI_USERNAME` - username of control-plane or bastion host
    * `PRIVATE_KEY` - private key for ssh access
