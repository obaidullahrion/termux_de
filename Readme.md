# configure termux with vnc

---

# **Setting Up JWM & Zsh Like Kali Linux (Termux Guide)**

### **1️⃣ Installing & Configuring JWM**

1. **Install JWM & Required Packages**
    
    ```
    
    pkg install jwm x11-repo feh  xclip xsel  -y
    ```
    
2. **Create JWM Config File**
    
    ```
    nano ~/.jwm/jwmrc
    ****
    
    ```
    
3. **Modify `~/.jwmrc` with:**
    - **Taskbar** (Bottom)
    - **Firefox & QTerminal**
    - **Right-click for Menu**
    - **Wallpaper Support**
    
    ```xml
    <JWM>
    
        <!-- Set Wallpaper ->
        <StartupCommand>feh --bg-scale ~/wall.jpg</StartupCommand>
    
        <!-- Enable Clipboard -->
        <StartupCommand>xsel --clipboard --nodetach</StartupCommand>
    
        <!-- Taskbar (Bottom Panel, Kali Style) -->
        <Tray x="0" y="-1" height="28">
            <!-- Start Menu Button -->
            <TrayButton label="☰">root:3</TrayButton>
    
            <!-- Pinned Apps -->
            <TrayButton label="🖥 Terminal">exec:qterminal</TrayButton>
            <TrayButton label="🌐 Firefox">exec:firefox</TrayButton>
    
            <!-- Running Apps (Icons Only) -->
            <TaskList labeled="false"/>
    
            <!-- Workspace Switcher -->
            <Pager/>
    
            <!-- Logout Button -->
            <TrayButton label="⏻">exit</TrayButton>
        </Tray>
    
        <!-- Workspaces (2 Desktops) -->
        <Desktops width="2" height="1">
            <Background type="solid">#222222</Background>
        </Desktops>
    
        <!-- Keyboard Shortcuts -->
        <Key key="F1">exec:qterminal</Key>
        <Key key="F2">exec:firefox</Key>
    
        <!-- Right-Click Menu (Start Menu, Like Kali) -->
        <RootMenu onroot="3">
            <Menu label="Applications">
                <Menu label="Accessories">
                    <Program label="File Manager">pcmanfm</Program>
                    <Program label="Text Editor">nano</Program>
                    <Program label="Calculator">galculator</Program>
                </Menu>
                <Menu label="Internet">
                    <Program label="Firefox">firefox</Program>
                </Menu>
                <Menu label="System">
                    <Program label="Terminal">qterminal</Program>
                    <Program label="Task Manager">htop</Program>
                </Menu>
            </Menu>
            <Separator/>
            <Restart label="Restart JWM"/>
            <Exit label="Logout"/>
        </RootMenu>
    
    </JWM>
    
    ```
    
4. **to Apply Changes**
    
    ```
    
    jwm -restart
    
    ```
    

---

- **Configure vnc with jwm**
After the server is set up, configure it to use **JWM** as the window manager. Create or edit the `.vnc/xstartup` file to configure the window manager:
    
    ```bash
    
    nano ~/.vnc/xstartup
    
    ```
    
    Add the following lines to start JWM:
    
    ```bash
    
    #!/bin/sh
    xrdb $HOME/.Xresources
    xsetroot -solid grey
    export XDG_SESSION_TYPE=x11
    export XDG_CURRENT_DESKTOP=GNOME
    jwm &
    
    ```
    
- **Start the VNC Server with JWM**
Restart the VNC server to apply the changes:
    
    ```bash
    
    vncserver -kill :1
    vncserver :1
    
    ```
    

### **2️⃣ Installing & Configuring Zsh (Kali Style)**

1. **Install Zsh**
    
    ```bash
    
    pkg install zsh -y
    
    git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions\ngit clone https://github.com/zsh-users/zsh-syntax-highlighting ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting\n
    chsh -s zsh
    
    git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions
    
    git clone https://github.com/zsh-users/zsh-syntax-highlighting ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
    
    ```
    
2. **Set Kali-style Prompt**Add this line:Apply:
    
    ```
    nano ~/.zshrc
    
    ```
    
    paste this in the file
    
    ```
    
    # If you come from bash you might have to change your $PATH.
    # export PATH=$HOME/bin:$HOME/.local/bin:/usr/local/bin:$PATH
    
    # Path to your Oh My Zsh installation.
    export ZSH="$HOME/.oh-my-zsh"
    
    # Set name of the theme to load --- if set to "random", it will
    # load a random theme each time Oh My Zsh is loaded, in which case,
    # to know which specific one was loaded, run: echo $RANDOM_THEME
    # See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
    ZSH_THEME="agnoster"
    
    # Set list of themes to pick from when loading at random
    # Setting this variable when ZSH_THEME=random will cause zsh to load
    # a theme from this variable instead of looking in $ZSH/themes/
    # If set to an empty array, this variable will have no effect.
    # ZSH_THEME_RANDOM_CANDIDATES=( "robbyrussell" "agnoster" )
    
    # Uncomment the following line to use case-sensitive completion.
    # CASE_SENSITIVE="true"
    
    # Uncomment the following line to use hyphen-insensitive completion.
    # Case-sensitive completion must be off. _ and - will be interchangeable.
    # HYPHEN_INSENSITIVE="true"
    
    # Uncomment one of the following lines to change the auto-update behavior
    # zstyle ':omz:update' mode disabled  # disable automatic updates
    # zstyle ':omz:update' mode auto      # update automatically without asking
    # zstyle ':omz:update' mode reminder  # just remind me to update when it's time
    
    # Uncomment the following line to change how often to auto-update (in days).
    # zstyle ':omz:update' frequency 13
    
    # Uncomment the following line if pasting URLs and other text is messed up.
    # DISABLE_MAGIC_FUNCTIONS="true"
    
    # Uncomment the following line to disable colors in ls.
    # DISABLE_LS_COLORS="true"
    
    # Uncomment the following line to disable auto-setting terminal title.
    # DISABLE_AUTO_TITLE="true"
    
    # Uncomment the following line to enable command auto-correction.
    # ENABLE_CORRECTION="true"
    
    # Uncomment the following line to display red dots whilst waiting for completion.
    # You can also set it to another string to have that shown instead of the default red dots.
    # e.g. COMPLETION_WAITING_DOTS="%F{yellow}waiting...%f"
    # Caution: this setting can cause issues with multiline prompts in zsh < 5.7.1 (see #5765)
    # COMPLETION_WAITING_DOTS="true"
    
    # Uncomment the following line if you want to disable marking untracked files
    # under VCS as dirty. This makes repository status check for large repositories
    # much, much faster.
    # DISABLE_UNTRACKED_FILES_DIRTY="true"
    
    # Uncomment the following line if you want to change the command execution time
    # stamp shown in the history command output.
    # You can set one of the optional three formats:
    # "mm/dd/yyyy"|"dd.mm.yyyy"|"yyyy-mm-dd"
    # or set a custom format using the strftime function format specifications,
    # see 'man strftime' for details.
    # HIST_STAMPS="mm/dd/yyyy"
    
    # Would you like to use another custom folder than $ZSH/custom?
    # ZSH_CUSTOM=/path/to/new-custom-folder
    
    # Which plugins would you like to load?
    # Standard plugins can be found in $ZSH/plugins/
    # Custom plugins may be added to $ZSH_CUSTOM/plugins/
    # Example format: plugins=(rails git textmate ruby lighthouse)
    # Add wisely, as too many plugins slow down shell startup.
    plugins=(git zsh-autosuggestions zsh-syntax-highlighting )
    
    source $ZSH/oh-my-zsh.sh
    
    # User configuration
    
    # export MANPATH="/usr/local/man:$MANPATH"
    
    # You may need to manually set your language environment
    # export LANG=en_US.UTF-8
    
    # Preferred editor for local and remote sessions
    # if [[ -n $SSH_CONNECTION ]]; then
    #   export EDITOR='vim'
    # else
    #   export EDITOR='nvim'
    # fi
    
    # Compilation flags
    # export ARCHFLAGS="-arch $(uname -m)"
    
    # Set personal aliases, overriding those provided by Oh My Zsh libs,
    # plugins, and themes. Aliases can be placed here, though Oh My Zsh
    # users are encouraged to define aliases within a top-level file in
    # the $ZSH_CUSTOM folder, with .zsh extension. Examples:
    # - $ZSH_CUSTOM/aliases.zsh
    # - $ZSH_CUSTOM/macos.zsh
    # For a full list of active aliases, run `alias`.
    #
    # Example aliases
    # alias zshconfig="mate ~/.zshrc"
    # alias ohmyzsh="mate ~/.oh-my-zsh"
    PROMPT=$'%F{cyan}┌──(%F{cyan}%n@%m%F{cyan})-[%F{cyan}%~%F{cyan}]\n└─%F{cyan}$%f '
    
    ```
    
    ```
    
    source ~/.zshrc
    
    ```
    

---

---

### **mannualy Setting Wallpaper if automatically doesnt work**

```xml
feh --bg-scale ~/wall.png

```
