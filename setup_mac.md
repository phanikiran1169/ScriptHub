# My macOS software installation guide

Follow the steps below to install essential software on macOS.

---

## Step 1: Install Homebrew
Homebrew is a package manager for macOS. Run the following command to install Homebrew:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

---

## Step 2: Install cURL
After installing Homebrew, use it to install cURL:
```bash
brew install curl
```

---

## Step 3: Install Wget
Use Homebrew to install Wget:
```bash
brew install wget
```

---

## Step 4: Install Git
Install Git using Homebrew:
```bash
brew install git
```

---

## Step 5: Install Visual Studio Code
1. Download and install Visual Studio Code from the official website:  
   [Download Visual Studio Code](https://code.visualstudio.com)

2. To use the `code` command in the terminal, add Visual Studio Code to your `$PATH` environment variable.  
   Run the following command to add it:
   ```bash
   export PATH=$PATH:/Applications/Visual\ Studio\ Code.app/Contents/Resources/app/bin
   ```

3. Save this change permanently by adding the above line to your shell configuration file. Use one of the following commands based on your shell:
   - For `zsh` (default shell on macOS Catalina and later):
     ```bash
     echo 'export PATH=$PATH:/Applications/Visual\ Studio\ Code.app/Contents/Resources/app/bin' >> ~/.zshrc
     source ~/.zshrc
     ```

---
