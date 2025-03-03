# configure termux with vnc

---

# **Setting Up JWM & Zsh Like Kali Linux (Termux Guide)**

### **1️⃣ Installing & Configuring JWM**

1. **Install JWM & Required Packages**
    
    ```
    
    pkg install jwm xsel x11-repo feh tigervnc -y
    ```
    
    
3. **create and Modify `~/.jwmrc` with:**
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
    

    '''#!/bin/sh
xrdb $HOME/.Xresources
xsetroot -solid grey
export XDG_SESSION_TYPE=x11
export XDG_CURRENT_DESKTOP=JWM  # Change this from GNOME to JWM

# Add feh to set the wallpaper
feh --bg-scale ~/wallpaper.jpg &

exec jwm
'''
    
- **Start the VNC Server with JWM**
Restart the VNC server to apply the changes:
    
    ```bash
    
    vncserver -kill :1
    vncserver :1
    
    ```


    
### **mannualy Setting Wallpaper if automatically doesnt work**

```xml
feh --bg-scale ~/wall.png

```



