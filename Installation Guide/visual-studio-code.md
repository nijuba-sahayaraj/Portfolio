
# Installation Guide for Visual Studio Code

**Visual Studio Code (VS Code)** is a free, powerful, and lightweight source code editor developed by Microsoft. It supports development operations like debugging, task running, and version control.

Website: [https://code.visualstudio.com/](https://code.visualstudio.com/)

---

## Table of Contents

1. [Downloading VS Code](#downloading-vs-code)
2. [Installing on Windows](#installing-on-windows)
3. [Installing on macOS](#installing-on-macos)
4. [Installing on Linux](#installing-on-linux)
5. [Verifying the Installation](#verifying-the-installation)
6. [Installing Extensions](#installing-extensions)

---

## Downloading VS Code

1. Visit the official website: [https://code.visualstudio.com/](https://code.visualstudio.com/)
2. Click on the **Download** button.
3. Select your operating system:  
   - **Windows**
   - **macOS**
   - **Linux (Debian/Ubuntu/RHEL/Fedora/others)**

---

## Installing on Windows

1. Download the `.exe` installer.
2. Run the installer.
3. Follow the setup wizard:
   - Accept the license agreement.
   - Choose the installation location.
   - Select additional tasks (e.g., "Add to PATH", "Register code as an editor").
4. Click **Install**.
5. Launch VS Code after the installation is complete.

---

## Installing on macOS

1. Download the `.zip` file.
2. Open the `.zip` to extract the `Visual Studio Code.app`.
3. Move the app to the `/Applications` folder.
4. (Optional) Open Terminal and run:
   ```bash
   sudo ln -s /Applications/Visual\ Studio\ Code.app/Contents/Resources/app/bin/code /usr/local/bin/code 
   ```
      This enables launching VS Code from the terminal using the `code` command.

## Installing on Linux

### Debian/Ubuntu

```bash
sudo apt update
sudo apt install wget gpg
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /usr/share/keyrings/
sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] \
https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt update
sudo apt install code
```

### RHEL/Fedora

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\
\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > \
/etc/yum.repos.d/vscode.repo'
sudo dnf check-update
sudo dnf install code
```

## Verifying the Installation

To confirm VS Code is installed successfully:

+ **Launch the application:**

    + Windows: Start Menu → Visual Studio Code

    + macOS: Applications → Visual Studio Code

    + Linux: Application Launcher → Visual Studio Code

+ **Check version from Terminal/Command Prompt:**

```bash
code --version
```

## Installing Extensions

1. Open VS Code.

2. Click on the Extensions icon in the Activity Bar on the side.

2. Search for extensions (e.g., Python, Prettier, ESLint).

4. Click Install next to the desired extension.

Alternatively, use the terminal:

```
code --install-extension ms-python.python
```

## Additional Resources


- [Official VS Code Documentation](https://code.visualstudio.com/docs)  


- [Marketplace Extensions](https://marketplace.visualstudio.com/vscode)  



