# Use an official Ubuntu as the base image
FROM ubuntu:18.04

ARG <YOUR IP ADDRESS>

ENV DISPLAY ${HOST_IP}:0.0

RUN apt update

# Install necessary packages (including systemd, Snapd, Tcl, and others)
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y systemd snapd tcl wget

# Enable systemd
RUN systemctl enable snapd.service

# Install nam and ns2 with auto-accepting prompts
RUN printf 'y\ny\n6\n44\n' | apt-get install nam ns2

# Download sample Tcl code
RUN wget http://nile.wpi.edu/NS/Example/ns-simple.tcl

# Necessary packages for X11 support
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y xdg-utils

RUN apt install tclsh -y


# Start systemd on container startup
CMD ["/lib/systemd/systemd"]