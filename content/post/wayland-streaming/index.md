---
title: Improved Wayland Screen Sharing
description: How to Fix Apps Like Discord to Stream on Wayland
slug: wayland-streaming
date: 2023-10-19 00:00:00+0000
image: cover.png
categories:
    - Guide
tags:
    - Guide
    - Wayland
    - Linux
    - X
weight: 1
---

# How to Use x Apps That Cannot Capture Your Screen on Wayland

Gone are the days when you couldn't stream your screen on apps like Discord. Let me introduce you to a nifty tool called xwaylandvideobridge. It's incredibly straightforward to set up and packs a punch in terms of functionality. So, grab a cup of tea, take a seat, and i will accompany you on this journey of seamless screen sharing with your friends on a modern graphics stack.


## Installation

### Step 1 Downloading

1. First, head over to [xwaylandvideobridge on KDE GitLab](https://invent.kde.org/system/xwaylandvideobridge).
2. On the left sidebar, click on "CI/CD." 
3. Download the latest Flatpak archive artifact and unzip it. (Note: If the latest release doesn't have any artifacts, proceed with the a older Release.)

### Step 2 Installing

1. Ensure you have Flatpak and Flathub installed. (If you haven't, visit [Flathub setup](https://flathub.org/setup).)
2. Open a terminal and navigate to your Downloads Folder.
3. Execute the following command:
    ```bash
    flatpak install xwaylandvideobridge.flatpak
    ```
4. If prompted, type 'Y' and enter your password when necessary.

5. Once the installation is complete, you can launch the program by running:
    ```bash
    flatpak run org.kde.xwaylandvideobridge 
    ```

### Step 3 Autostart (optional)

1. You can create a new text file named "videobridge.sh." You can do this using a text editor or through the command line. For instance, in the terminal, you can use the following command to create the file:

    ```bash
    touch videobridge.sh
    ```

2. Open the "videobridge.sh" file with a text editor of your choice, such as nano, vim, or gedit. For example:

    ```bash
    nano videobridge.sh
    ```

3. In the "videobridge.sh" file, insert the following line:

    ```bash
    flatpak run org.kde.xwaylandvideobridge
    ```

4. Save and close the file in your text editor. If you're using nano, you can save by pressing Ctrl + O, then press Enter, and exit by pressing Ctrl + X.

5. Now, you'll need to add the "videobridge.sh" script to your desktop environment's autostart configuration. The process may vary depending on your desktop environment.

   In KDE:
   - Open "System Settings."
   - Navigate to "Startup and Shutdown." > "Autostart"
   - Click "Add Script."
   - Browse and select the "videobridge.sh" script you created.
   - Save your changes, and the script will run automatically with every session.

   For other desktop environments or window managers, there are similar ways to accomplish this.

## How to Use It

Once you've started the application, every time you attempt to capture a window or your screen, a window will appear where you can choose the source of the video stream. After selecting one, xwaylandvideobridge should display a window that you can capture in the program you are using. I've mainly tested this with Discord, and it works virtually bug-free with excellent performance. Give it a try!
