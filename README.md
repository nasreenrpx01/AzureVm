# **Configuring IIS on Azure VMs**

## **Project Overview**
This project demonstrates the process of setting up **Internet Information Services (IIS)** on **Windows Virtual Machines (VMs)** and **Nginx/Apache** on **Linux VMs** in **Microsoft Azure**. The primary objective was to automate the configuration process and optimize web services for high availability and performance. 

The project uses **PowerShell** scripts for Windows VM automation and **Nginx/Apache** configuration for Linux VMs. This configuration ensures smooth web hosting for applications hosted on Azure infrastructure.

## **Table of Contents**
- [Technologies Used](#technologies-used)
- [Project Setup](#project-setup)
- [Steps for Windows VM (IIS)](#steps-for-windows-vm-iis)
- [Steps for Linux VM (Nginx/Apache)](#steps-for-linux-vm-nginxapache)
- [Automation](#automation)
- [High Availability and Performance Optimization](#high-availability-and-performance-optimization)
- [Conclusion](#conclusion)

## **Technologies Used**
- **Azure VMs**: Scalable virtual machines that host web applications and services.
- **IIS (Internet Information Services)**: A web server for Windows VMs to host websites and applications.
- **PowerShell**: Scripting language used to automate the configuration of IIS on Windows VMs.
- **Nginx/Apache**: Web servers for Linux VMs to host websites and services.
- **Linux**: Open-source operating system used for the Linux-based VM hosting.

## **Project Setup**

To get started with this project, you need an active **Azure subscription** and access to **Azure Portal**.

### Prerequisites
- **Azure Subscription**: Create an Azure account if you don't have one already.
- **PowerShell**: Required for automating IIS configuration on Windows VMs.
- **SSH Key**: Used for connecting to the Linux VMs.
- **Azure CLI**: Install Azure CLI to manage resources via command-line.
  
### Steps to Deploy Azure VMs
1. **Create Virtual Machines in Azure:**
   - Create two VMs in Azure, one for Windows and one for Linux.
   - For Windows VM, use **Windows Server** image.
   - For Linux VM, use **Ubuntu** or another preferred Linux distribution.
   
2. **Configure Networking & Security:**
   - Ensure the VMs are properly connected to a **Virtual Network (VNet)**.
   - Open the required **ports** (e.g., 80, 443 for HTTP and HTTPS) in the **Network Security Group (NSG)**.

3. **Access VMs:**
   - Use **RDP (Remote Desktop Protocol)** for Windows VMs.
   - Use **SSH** to connect to Linux VMs.

## **Steps for Windows VM (IIS)**

### Manual Configuration:
1. **Install IIS** on Windows VM:
   - Open **Server Manager** > Click on **Add Roles and Features**.
   - Select **Web Server (IIS)** and complete the installation process.

2. **Configure IIS Settings**:
   - Launch the **IIS Manager**.
   - Configure the web server to host your site.

### Automation with PowerShell:
1. **PowerShell Script to Install IIS**:
   ```powershell
   Install-WindowsFeature -name Web-Server -IncludeManagementTools
   ```
   This script installs IIS along with management tools.

2. **Configure IIS for a Web App**:
   You can configure IIS to host your web applications by creating a new **site** in IIS Manager or automating it through PowerShell.
   
   Example script to create a website:
   ```powershell
   New-Website -Name "MyWebApp" -Port 80 -HostHeader "mywebsite.com" -PhysicalPath "C:\inetpub\wwwroot"
   ```

## **Steps for Linux VM (Nginx/Apache)**

### Manual Configuration:
1. **Install Nginx or Apache on Linux VM**:
   ```bash
   sudo apt-get update
   sudo apt-get install nginx  # For Nginx
   sudo apt-get install apache2  # For Apache
   ```

2. **Start and Enable Nginx/Apache Service**:
   ```bash
   sudo systemctl start nginx   # Start Nginx
   sudo systemctl enable nginx  # Enable Nginx to run at startup
   ```

3. **Configure Nginx/Apache for Web Hosting**:
   - Create a server block in Nginx or a virtual host in Apache.
   - Point it to the desired web application directory.

### Automation with Scripts:
1. **Script to Install Nginx and Configure Website**:
   ```bash
   sudo apt-get update
   sudo apt-get install -y nginx
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```
   Modify the Nginx config file to set the correct root directory for your application.

## **Automation**

- **PowerShell for Windows**: Automates the installation and configuration of IIS.
- **Shell scripts for Linux**: Automates the installation and setup of **Nginx/Apache**.
  
**Example PowerShell script for Windows** automates IIS installation:
```powershell
Install-WindowsFeature Web-Server, Web-WebServer, Web-Common-Http
```

**Shell script for Linux** automates Nginx installation:
```bash
#!/bin/bash
sudo apt update
sudo apt install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx
```

## **High Availability and Performance Optimization**
- **Load Balancing**: For high availability, use **Azure Load Balancer** to distribute traffic across multiple VMs.
- **Autoscaling**: Implement autoscaling to automatically adjust the number of VMs based on traffic.
- **Caching**: Use caching strategies (e.g., Nginx caching) to improve web performance.
- **Monitoring**: Use **Azure Monitor** and **Log Analytics** to track VM performance and health.

## **Conclusion**

This project demonstrates how to configure and optimize web services on **Windows and Linux VMs in Azure**. By automating the installation of IIS and configuring web servers like Nginx and Apache, the setup process becomes easier, and it ensures **high availability** and **performance** of your hosted web applications.

You can use this setup as a foundation for deploying scalable web applications on **Azure**.

