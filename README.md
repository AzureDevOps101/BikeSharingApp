# Bike Sharing Sample: Iteratively Develop and Debug Microservices in Kubernetes

## Quickstart
[Quickstart: Team development on Kubernetes using Azure Dev Spaces](https://docs.microsoft.com/en-us/azure/dev-spaces/quickstart-team-development).


## Demo Script

1. Prep AKS

```shell
az group create --name MyResourceGroup --location southeastasia

az aks create -g MyResourceGroup -n MyAKS --location southeastasia --node-vm-size Standard_DS2_v2 --node-count 1 --disable-rbac --generate-ssh-keys

az aks use-dev-spaces -g MyResourceGroup -n MyAKS --space dev --yes
```

Add current azure user account into DevSpaceControllers' owner group


2. Helm Install

```shell
cd /BikeSharingApp/

$ azds show-context

Name                ResourceGroup     DevSpace  HostSuffix
------------------  ----------------  --------  -----------------------
MyAKS               MyResourceGroup   dev       fedcab0987.eus.azds.io
```

Replace <REPLACE_ME_WITH_HOST_SUFFIX> with HostSuffix

```shell
cd charts/
helm init --wait
helm install -n bikesharing . --dep-up --namespace dev --atomic --wait
```
Wait for the install finishes

```
$ azds list-uris
Uri                                                 Status
--------------------------------------------------  ---------
http://dev.bikesharingweb.fedcab0987.eus.azds.io/  Available
http://dev.gateway.fedcab0987.eus.azds.io/         Available
```

3. Create more dev spaces

```shell
azds space select -n dev/azureuser1 -y
azds space select -n dev/azureuser2 -y
```

Switch to `dev/azureuser2` then use vscode open /BikeSharingWeb/ folder

make sure you have Azure Dev Space extension installed

Press F1 and select "Prepare configuration files for Dev Spaces"

in vscode, press debug button.