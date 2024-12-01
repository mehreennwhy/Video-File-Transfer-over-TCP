# Video-File-Transfer-over-TCP
This project implements a sender/receiver program to transmit video files over TCP sockets using GNU C on a Linux operating system. It also includes a simple GUI for selecting video files and monitoring the transfer status.

## Table of Contents  

- [Overview](#overview)  
- [Requirements](#requirements)  
- [Features](#features)  
- [Implementation Details](#implementation-details)  
- [Installation](#installation)  
- [Usage](#usage)  
- [Code Structure](#code-structure)  
- [Future Enhancements](#future-enhancements)

## Overview  

The project implements:  
1. A sender program with a GUI for selecting and sending video files over TCP sockets.  
2. A receiver program that accepts the video file, reconstructs it, and saves it to disk.  
3. File transfer status displayed in real-time using a progress bar in the sender GUI.  

---

## Requirements  

- **Operating System**: Linux  
- **Programming Language**: GNU C  
- **Libraries**:  
  - GTK+3 (for GUI)  
  - Standard TCP/IP socket libraries  

---

## Features  

### Sender  
- Graphical User Interface (GUI):  
  - File chooser for video selection.  
  - Progress bar to show transfer status.  
  - Status messages for user feedback.  
- Opens the target folder upon transfer completion.  
- Sends the video file in segments over TCP.  
- Sends an EOF signal to mark the end of the file.  

### Receiver  
- Accepts file segments and reconstructs the video file.  
- Identifies EOF signal to terminate transfer.  
- Saves the file with the name `received_video.mp4`.  
- Automatically plays the video using VLC after transfer completion.  

---

## Implementation Details  

### Sender  
The sender:  
1. Opens and reads the selected video file.  
2. Sends file data in chunks using TCP.  
3. Tracks and displays transfer progress in the GUI.  
4. Sends an EOF signal upon completing the transfer.  

### Receiver  
The receiver:  
1. Waits for incoming connections on a specified port (default: 8080).  
2. Receives file chunks and writes them to `received_video.mp4`.  
3. Identifies the EOF signal and closes the file.  
4. Plays the received video file using VLC.

---

## Installation  

### 1. Clone the Repository  
Open a terminal and clone the repository using:  
git clone https://github.com/your-repo-name.git
cd your-repo-name

### 2.Install Dependencies
Ensure required libraries are installed:
sudo apt-get update
sudo apt-get install libgtk-3-dev vlc 

### 3.Compile the Sender Program
Compile the sender code using GCC:
gcc sender.c -o sender `pkg-config --cflags --libs gtk+-3.0`

### 4.Compile the Receiver Program
Compile the receiver code:
gcc receiver.c -o receiver

### 5.Verify Setup
Ensure both executables (sender and receiver) are created in the project directory.

---

## Usage
### Step 1: Start the Receiver
On one terminal, run the receiver:
./receiver

### Step 2: Start the Sender
On another terminal, run the sender:
./sender

### Step 3: Select and Transfer a Video File
Use the GUI to choose a video file from your directory.
Monitor transfer progress on the progress bar.
Once the transfer completes, the target folder opens automatically.

### Step 4: Play the Received Video
The receiver saves the file as received_video.mp4 in the current directory.
VLC automatically plays the received video after the transfer.

---

## Code Structure
sender.c: Contains code for the sender program, including GUI and file transmission logic.
receiver.c: Implements the receiver to accept file data, save it, and play the video.

---

## Further Information

### Networking Details
Protocol: TCP is used for reliable communication.
Port: The default port is 8080. You can change it in the code if needed.
EOF Handling: The sender sends an "EOF" signal to mark the end of the file.

### GUI Features
The sender's GUI is built using GTK+3 and includes:

A file chooser dialog to select video files.
A progress bar updated in real-time as the file transfers.
A label displaying percentage progress and transfer completion messages.

## Limitations
The program assumes the receiver is always ready to accept the file.
The default video player is VLC; ensure it is installed and accessible via terminal.
