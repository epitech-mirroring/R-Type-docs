# R-Type Reborn User Guide

Welcome to the R-Type Reborn User Guide! Follow these instructions to get started with installing and running the game.

### Step 1: Downloading R-Type Reborn
You can download the latest version of R-Type Reborn from the official GitHub releases page:
[R-Type Reborn Releases](https://github.com/epitech-mirroring/R-Type-Reborn/releases/tag/v0.1.0)

Available downloads:
- **R-Type-Reborn-0.1.0-Linux.rpm**: Installer for Fedora Linux (includes both client and server).
- **R-Type-Reborn-0.1.0-win64.exe**: Windows installer (includes both client and server).
- **R-Type-Reborn-Client-x86_64.AppImage**: Portable client application for Linux.
- **R-Type-Reborn-Server-x86_64.AppImage**: Portable server application for Linux.

### Step 2: Choosing the Right Version
- **Windows Users**: Download the `R-Type-Reborn-0.1.0-win64.exe` to easily install both the client and server applications.
- **Linux Users**:
    - If you use **Fedora**, choose the `R-Type-Reborn-0.1.0-Linux.rpm` file to install the application with minimal effort.
    - For all other Linux systems, use the `AppImage` files. The `AppImage` files are portable and do not require installation, making them compatible across various Linux distributions.

### Step 3: Installing the Application
- **Windows**: Run the installer `R-Type-Reborn-0.1.0-win64.exe` and follow the prompts. After installation, the icons for the client and server will appear on your desktop.

- **Linux**:
    - **Fedora**: Double-click the `.rpm` file to install the application. The client and server will be installed in `/usr/local`.
    - **AppImage**: There is no installation required. Simply download the AppImage files and you are ready to run them.

### Step 4: Running the Application
- **Windows**:
    - Double-click the desktop icons to run the server first, and then run the client after.

- **Linux**:
    - **Fedora**:
        - Open a terminal and navigate to `/usr/local`:
          ```bash
          cd /usr/local
          ```
        - Run the server first with:
          ```bash
          ./r-type_server <tcp_port> <udp_port>
          ```
        - Run the client after:
          ```bash
          ./r-type_client
          ```
        - Provide the correct server information on the screen to connect.
    - **AppImage**:
        - Open a terminal in the directory where the AppImage files are located.
        - Run the server first:
          ```bash
          ./R-Type-Reborn-Server-x86_64.AppImage <tcp_port> <udp_port>
          ```
        - Run the client after:
          ```bash
          ./R-Type-Reborn-Client-x86_64.AppImage
          ```

### Connecting the Client to the Server
To connect the client to the server, follow the steps below:
1. Launch the client and you will see the screen shown below:

    ![Client Screen](images/client_screen.png)

2. Enter the following information:
    - **Server IP**: The IP address of the server you wish to connect to.
    - **Server TCP Port**: The port used by the server for TCP communication.
    - **Server UDP Port**: The port used by the server for UDP communication.

3. Click **Connect** to establish a connection to the server.

Ensure that the server is already running before attempting to connect with the client.

