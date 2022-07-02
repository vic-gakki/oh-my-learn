
### Prerequisites
>windows 10 version 2004 and higher(Build 19041 and higher) or Windows 11. use **winver** to check version

### Install

#### Auto install
> wsl --install (using **administrator**)
> wsl --install -d <distroName>

#### Manually install
1. enable windows subsystem for linux `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`
2. check windows version for running wsl 2
3. enable virtual machine feature `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart` and then **restart** 
4. download linux kernel and install
5. set wsl 2 as default version `wsl --set-default-version 2`
6. install linux distribution in **Microsoft Store**


#### File storage
- open wsl project in windows file explorer `explorer.exe .`
- in WSL distribution command line to access windows file directory `/mnt/driver/dir`

#### Set up vs code
- get extension pack **Remote Development**
- update linux distribution
  - update `sudo apt update`
  - install wget to **retrieve content from web servers** and ca-certificates to **allow SSL-based applications to check for the authenticity of SSL connections** `sudo apt install wget ca-certificates`
- open remote project
  - in command line, cd to the project dir `code .`
  - in vscode, open command palette `remote-wsl`


#### Install node
  - to install nvm `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/release version/install.sh | bash`
  - to install lts version `nvm install --lts`

#### Basic commands of WSL
  - https://docs.microsoft.com/zh-cn/windows/wsl/basic-commands

#### Troubleshooting
  - [WSL2 common tips and tricks](https://blogs.subhamk.com/pages/wsl2.html)
  - [change install dir using LxRunOffline](https://blog.csdn.net/farer_yyh/article/details/113785474)
