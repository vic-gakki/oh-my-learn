# zsh 

### Install
> sudo apt install zsh

### Set up zsh as default
> command: **chsh -s \$(which zsh)** 
> use `echo $SHELL` or `$SHELL --version` to check

---

# oh-my-zsh

### Install
> wget: `sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

### Config
* .zshrc can config themes and plugins and alias. [antfu's setting](https://github.com/antfu/dotfiles/blob/main/.zshrc)
* font setting
  * if in wsl, should install in windows first [how to install in windows](https://slmeng.medium.com/how-to-install-powerline-fonts-in-windows-b2eedecace58) and then change the terminal font and code editor(vs code) font `"editor.fontFamily": "installed first, default"`


# Troubleshooting
  - git connection refused or timeout
    - get the ip address of the server [here](https://www.ipaddress.com/)  
    - change **hosts** file by adding ip address and domain name
