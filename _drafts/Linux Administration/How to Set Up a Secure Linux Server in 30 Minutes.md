# How to Set Up a Secure Linux Server in 30 Minutes

## Introduction

Setting up a secure Linux server is crucial for protecting your data and applications. This guide will show you how to configure a secure Linux server in just 30 minutes.

## Prerequisites

- Basic knowledge of Linux command-line interface
- A fresh installation of a Linux distribution (e.g., Ubuntu, CentOS)

## Step 1: Update and Upgrade the System

1. Update the package list:
   ```sh
   sudo apt update
   ```
2. Upgrade installed packages:
   ```sh
   sudo apt upgrade -y
   ```

## Step 2: Create a New User

1. Add a new user:
   ```sh
   sudo adduser newuser
   ```
2. Grant administrative privileges:
   ```sh
   sudo usermod -aG sudo newuser
   ```

## Step 3: Configure SSH

1. Install OpenSSH Server:
   ```sh
   sudo apt install openssh-server -y
   ```
2. Disable root login:
   ```sh
   sudo nano /etc/ssh/sshd_config
   ```
   Find the line `PermitRootLogin` and set it to `no`.
3. Restart SSH service:
   ```sh
   sudo systemctl restart ssh
   ```

## Step 4: Set Up a Firewall

1. Install UFW (Uncomplicated Firewall):
   ```sh
   sudo apt install ufw -y
   ```
2. Allow SSH connections:
   ```sh
   sudo ufw allow OpenSSH
   ```
3. Enable the firewall:
   ```sh
   sudo ufw enable
   ```

## Step 5: Secure SSH with Fail2Ban

1. Install Fail2Ban:
   ```sh
   sudo apt install fail2ban -y
   ```
2. Start and enable Fail2Ban:
   ```sh
   sudo systemctl start fail2ban
   sudo systemctl enable fail2ban
   ```

## Step 6: Install and Configure Fail2Ban

1. Create a local configuration file:
   ```sh
   sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
   ```
2. Configure SSH jail:
   ```sh
   sudo nano /etc/fail2ban/jail.local
   ```
   Ensure the following settings:
   ```sh
   [sshd]
   enabled = true
   ```

## Summary

By following these steps, you’ve set up a secure Linux server in just 30 minutes. Regular maintenance and updates will help keep your server secure and running smoothly.

## Call to Action

Continue exploring advanced security configurations for your Linux server. Stay tuned for more articles on Linux server management and security best practices.
