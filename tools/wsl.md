
### Prerequisites
>windows 10 version 2004 and higher(Build 19041 and higher) or Windows 11. use **winver** to check version

### Install

#### Auto install
> wsl --install (using **administrator**)

#### Manually install
1. enable windows subsystem for linux `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`
2. check windows version for running wsl 2
3. enable virtual machine feature `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart` and then **restart** 
4. download linux kernel and install
5. set wsl 2 as default version `wsl --set-default-version 2`
6. install linux distribution in **Microsoft Store**


#### File storage
- open wsl project in windows file explorer `explorer.exe .`
- in WSL distribution command line to access windows file directory `/mnt/dirve/dir`

#### Set up vs code
- get extension pack **Remote Development**
- update linux distribution
  - update `sudo apt update`
  - install wget to **retrieve content from web servers** and ca-certificates to **allow SSL-based applications to check for the authenticity of SSL connections** `sudo apt install wget ca-certificates`
- open remote project
  - in command line, cd to the project dir `code .`
  - in vscode, open command palette `remote-wsl`


#### Others
  - wsl -l -v: to list all version
