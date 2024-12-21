# Installation Guide for Oh My Zsh on macOS

Oh My Zsh is an open-source, community-driven framework for managing your zsh configuration. It comes with many features out of the box and improves your terminal experience.

---

## Install Oh My Zsh

Run the following command to install Oh My Zsh:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

The installation script should set `zsh` as the default shell. It can also be set manually by:

```bash
chsh -s $(which zsh)
```

---

## Configuration

The out-of-the-box configuration is usable, but it would be better if we customize it to suit our needs. The [Official Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki) contains a lot of useful information if you want to deep dive into what you can do with Oh My Zsh.

To apply the changes you make, either start a new shell instance or run:

```bash
source ~/.zshrc
```

---

## Install PowerLevel10K Theme for Oh My Zsh

Clone the PowerLevel10K repository:
   
 ```bash
 git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
 ```

Update the following line in `~/.zshrc`

 ```bash
 ZSH_THEME="powerlevel10k/powerlevel10k"
 ```

---

## Install zsh-syntax-highlighting

The Syntax Highlighting plugin adds beautiful colors to the commands you type.

Clone the zsh-syntax-highlighting plugin’s repository and copy it to the “Oh My Zsh” plugins directory:

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

---

## Install zsh-autosuggestions

This plugin auto-suggests any of the previous commands
Clone the zsh-autosuggestions plugin’s repository and copy it to the “Oh My Zsh” plugins directory:

 ```bash
 git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
 ```

---

## Add Plugins

Add plugins to the shell by editing the `plugins` array in the `~/.zshrc` file:

```bash
plugins=(git zsh-autosuggestions zsh-syntax-highlighting web-search)
```

A list of all available plugins on the [Oh My Zsh Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins). Note that adding too many plugins may increase shell startup time.

---

## Enforce Changes

To apply the changes, either start a new shell instance or run:
```bash
source ~/.zshrc
```
