
---

# Docker Container Setup for NS2 on MAC

## Initial Setup

1. **Edit the Docker File**:
   - Locate the line:
     ```
     #ARG <YOUR IP ADDRESS>
     ```
   - Replace `<YOUR IP ADDRESS>` with your computer's IP address.

## Building the Docker Image

- Execute the following command to build the Docker image:
  ```
  docker build -t computer-networks-project-image .
  ```

## Running the Docker Container

1. **Pre-requisites**:
   - Ensure XQuartz is installed on your Mac.

2. **Run the Container**:
   - Replace `<YOUR IP ADDRESS>` with your machine's IP address in the following command:
     ```
     docker run -e DISPLAY=<YOUR IP ADDRESS>:0 --privileged --net=host --name computer-networks-project-env -d computer-networks-project-image
     ```

3. **Access the Container**:
   - Use this command to open the running container:
     ```
     docker exec -it -e DISPLAY=<Your IP Address>:0 computer-networks-project-env /bin/bash
     ```

## XQuartz Configuration

1. **Install X11 Apps**:
   - Inside the container, run:
     ```
     apt-get install x11-apps
     ```

2. **Enable Connections**:
   - On your Mac, go to XQuartz preferences:
     - Select `Preferences -> Security Tab`.
     - Ensure `Allow Connections from network clients` is checked.

## Testing X11 Forwarding

1. **Check Display Variable**:
   - Inside the container, run:
     ```
     echo $DISPLAY
     ```
   - Use the displayed value in the Xhost terminal command:
     ```
     xhost <Your IP ADDRESS>
     ```

2. **Test X11 Forwarding**:
   - To verify if forwarding is working, run:
     ```
     xclock
     ```
   - You should see a pop-up window if it is set up correctly.
