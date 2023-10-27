# Mikero Packer
This action will get a list of addons and manage to pack the modified ones for the [BRAF Mod](https://www.brafmod.com.br/) development pipeline, you can use it combined with another actiont to publish a release, upload it to the Steam Workshop or whatever.

**This actions presumes that:**  
* You are using a self-hosted runner with Windows environment
* Powershell 7+ installed (pwsh command)
* If you are going to obfuscate some addons, you have a valid mikero's paid pboproject installed and pointed as system variables
* You are using the following project folder structure:
```
  root_folder/
      addon1/
      addon2/
      addon3/
```
if you are using the CBA project structures (addons inside a addon folder) and do not need to obfuscate the addons, i strongly recommend you to use [HEMTT](https://github.com/arma-actions/hemtt) to get the job done

## Example
```
name: Build

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  build:
    runs-on: windows-latest
    defaults: { run: { shell: powershell } }
    steps:
    - uses: valmojr/mikero-packer
        env:
        - EXCLUDE_FROM_PBO: "" # default value, optional
        - EXCLUSION_MODIFIER: "" # default value, optional
        - KEY_DIRECTORY: # Won't sign in the addon if not provided
        - OUTPUT_DIRECTORY: "./release" # path where the addons will be outputted, if not defined, this example is de default value
```