## Deploy end-to-end HPC environment with CycleCloud | Azure HPC

### What are we building?
---
- A Virtual Network
- A Jumpbox acting as an NFS Server with 2TB of disks
- A BeeGFS parallel filesystem
- An Azure CycleCloud server with PBS integration and able to auto-scale virtual machines for HPC

### Setup azhpc CLI
---
- Download and install the latest version of **[jq](https://stedolan.github.io/jq/download/)**
- Download and install the latest version of **[Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)**
- Clone the Azure HPC repo
  - `git clone https://github.com/Azure/azurehpc.git`
- Source the install script
  - `. ./azurehpc/install.sh`

### Configure HPC deployment
---
- `mkdir demo_hpc`
- `cd demo_hpc`
- `cp ../azurehpc/examples/cc_beegfs/init.sh .`
- `cp ../azurehpc/examples/cc_beegfs/variables.json .`
- `ls`
- Edit` variables.json` to match the following:
```js{
  {
    "variables": {
      "resource_group": "demo_hpc",
      "location": "southcentralplus",
      "key_vault": "kv{{variables.uuid}}",
      "uuid": "demo_hpc",
      "projectstore": "locker{{variables.uuid}}",
      "scheduler": "pbs",
      "cc_image": "azurecyclecloud:azure-cyclecloud:cyclecloud-81:8.1.0",
      "cc_version": "8"
    }
  }
```
### Build config files
---
- Run `init.sh` to build config files from building blocks and global variables set in `variables.json`
  - `./init.sh`
  - `ls`

### Create a Resource Group, KeyVault and add CycleServer password
---
- `azhpc-build --no-vnet -c prereqs.json`

### References
---
- [Deploy end-to-end HPC environment with CycleCloud | Azure HPC](https://www.youtube.com/watch?v=_Hugv386nsg)
