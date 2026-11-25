# Executive Summary

This project converts an old laptop into an Ubuntu Server that provides DNS advertisement blocking, network monitoring, scheduled internet access control, security monitoring, and centralized log analysis. The server uses Pi-hole, Wazuh, and other open-source tools to improve the security and visibility of a home network.

# Project Introduction

## Background

Home network security protects personal data, devices, and online activities from unauthorized access and cyberattacks. Advertisements, trackers, malware, and unknown devices can invade privacy, slow the network, or steal sensitive information. Old hardware can be reused as a server for file storage, backups, media streaming, or network security tools at a low cost.

## Problems

* Advertisements and tracking domains

* Lack of visibility into connected devices

* No centralized security logs

* Devices using the internet after permitted hours

* Difficulty detecting suspicious activity

## Project Aims

The aim of this project is to build a centralized home network security and monitoring server using Ubuntu Server and open-source security tools. Controlling the connection of the other devices and adding a Parent Control System for the Home network Management.

## Project Objectives

* Insall Ubuntu Server on an old Headless Laptop that will be working as a server

* Configure The static IP for the Ubuntu Server in Ubuntu and from the WiFi modem

* Block Advertisement and tracking domains

* Monitor network devices and control internet access

* Block the selected Devices after 10 PM (to be implemented in the home router)

* Collect and Analyze security Logs

* Detect Suspicious Activity

* Secure Remote administration

* Back up important configuration files

# Requirement Analysis

## Functional Requirements

| ID | Requirements | Priority | Status |
| --- | --- | --- | --- |
| FR-01 | Block advertisement domains | High | Done |
| FR-02 | Display connected network devices | High | Done |
| FR-03 | Monitor device availability | High | Done |
| FR-04 | Block selected devices | High | Done |
| FR-05 | Disable internet after 10 PM | High | Done |
| FR-06 | Collect security logs | High | Done |
| FR-07 | Display SIEM alerts | High | Done |
| FR-08 | Back up configuration files | Medium | Not Started |

## Non-Functional Requirements

* Security

* Reliability

* Low cost

* Ease of administration

* Low power consumption

* Good performance

* Scalability

* Availability

* Maintainability

# Hardware Requirements

| Component | Specification |
| --- | --- |
| Processor | Intel Core i7-6600U |
| Physical cores | 2 |
| Logical Processor | 4 |
| RAM | 16 GB |
| Storage | Approximately 477 GB SSD |
| Graphics | Intel HD Graphics 520 |
| Architecture | 64-Bit |
| Network Interface | Wireless and Etherenet (Good) |
| Additional Adapter | N/A |
| Battery Condition | Good |

## Screenshots (when it was windows)

![Image 1](_project_0ct0pu5_images/image_001.png)
Figure : properties

![Image 2](_project_0ct0pu5_images/image_002.png)
Figure : specs

![Image 3](_project_0ct0pu5_images/image_003.png)
Figure : disk partition

# Software Requirements

| Software | Purpose | Version |
| --- | --- | --- |
| Ubuntu Server | Main operating system | 24.4.4 |
| Pi-Hole | DNS advertisement blocking | 6.4.3 |
| Unbound | Local Recursive DNS | Done locally |
| Wazuh | SIEM and endpoint monitoring | 3.10.2 |
| WireGaurd | Secure Remote Access | Converted to VPN instead |

# Implementation

## Disassembling the Laptop

The First step is to disassemble the laptop to remove the malfunctioning screen and use the laptop as a portable server.
![Image 4](_project_0ct0pu5_images/image_004.jpeg)
Figure

![Image 5](_project_0ct0pu5_images/image_005.jpeg)
Figure

![Image 6](_project_0ct0pu5_images/image_006.jpeg)
Figure

![Image 7](_project_0ct0pu5_images/image_007.jpeg)
Figure

![Image 8](_project_0ct0pu5_images/image_008.jpeg)
Figure

Now after Getting the Laptop with its last form (without the lid) connect the VGA to the screen and start installing Ubuntu version 24.4.4 by downloading the ISO and booting the system from a flash USB

Setting Up the hostname, and domain name including the FQDN (Fully Qualified Domain Name). The Next step is making the IP address of the server host Static; there 2 ways to make it either GUI (Grpahical User Interface) Or by command Line by changing the IP obtaining technique from automatic to manual then write the IP address of the server including the subnet mask and the Default Gateway (add any nuccessary IPs if nucessary like DHCP or DNS), click apply and save, if it is by command line then go for `/etc/NetworkManager/system-connection/<interface>` choose the desired interface to have a static IP address the change the method variable to manual and write the ip address with the same form of IP,subnet mask, default gateway.

# Installing Pi-Hole

Visite the official website of Pi-hole and download the installation files using a command they provide using github; start configuring the installation options and install. After done with installation you will be provided with a password and the link to you management page of Pi-hole use the password to sign in and you be redirected to the Dashboard.

![Image 9](_project_0ct0pu5_images/image_009.png)
Figure : Pi-Hole Dashboard

As the machine started it has collected 29 blocks from the default list it has, the next step is to add the list that contain the domains which shows the Ads

Now there is 2 main focus area "Domains" and "Lists" those 2 are the most important things in the software; the Domains sections is used to blacklist or whitelist the domains registered in that section, while the lists will be blacklisting or whitelisting the provided list of websites.

![Image 10](_project_0ct0pu5_images/image_010.png)
Figure : Domain

After the blocking starts the number increases;

![Image 11](_project_0ct0pu5_images/image_011.png)
Figure : Dashboard

Once every desired list is added the very next step is to update the gravity in order to make the Pi-Hole start blocking those domains which is stored in the list we uploaded just now.

![Image 12](_project_0ct0pu5_images/image_012.png)
Figure : Added the list

After clicking the update button, now the Ads start vanishing one after the another in websites (Youtube videos are not included) the reason for that is the "Youtube" has a technology that embedd the Ads into the video itself so it is not a seperate Ad video it is whole one video.

![Image 13](_project_0ct0pu5_images/image_013.png)
Figure : Updating the list

# Installing Wazuh

Wazuh was installed to provide centralized security monitoring for the home network. Its purpose is to collect security events from connected computers, analyze those events, and generate alerts when suspicious activity is detected.

The system was intended to provide the following functions:

* Centralized log collection

* Failed-login detection

* File-integrity monitoring

* Vulnerability detection

* System inventory

* Security alerting

* Monitoring of Windows and Linux computers

![Image 14](_project_0ct0pu5_images/image_014.png)
Figure : Disk PArtition linux

Checking the available disk and requirement for the “Wazuh Setup”

![Image 15](_project_0ct0pu5_images/image_015.png)
Figure : Wazuh installation

After the installation is done check the https page of the wazuh dashboard to check the other configuration staff. To keep in mind the port used for this service is 44344 and this information must not be written or shared with any other parties but as this is a simple isolated project I will share this information just to make sure that it goes step by step guidance using the command `sudo bash ./wazuh_install.sh -a -p 44344` and this will be enough.

![Image 16](_project_0ct0pu5_images/image_016.png)
Figure : creds

and got the credentials for the platform login page,

![Image 17](_project_0ct0pu5_images/image_017.png)
Figure : Wazuh Loading Page

Now after visiting the dashboard menu, the next step is to Deploy an agent by clicking the blue button, by this we will be able to add devices to the monitoring platform.

![Image 18](_project_0ct0pu5_images/image_018.png)
Figure : Wazuh Dashboard

![Image 19](_project_0ct0pu5_images/image_019.png)
Figure : System architecture

![Image 20](_project_0ct0pu5_images/image_020.png)
Figure : Name and configuration

![Image 21](_project_0ct0pu5_images/image_021.png)
Figure : copy paste command

The last step is to copy the command provided by wazuh and paste it in the specified device the command must be executed as an Administrator, then wait for a while the device will be connecting to the server.

![Image 22](_project_0ct0pu5_images/image_022.png)
Figure : Successful additon of device

device connected successfully.

![Image 23](_project_0ct0pu5_images/image_023.png)
Figure : Monitoring started

The monitoring start and each event or action taken in that device will be reported in this dashboard for that specific device and more devices can be added to be monitored as well, there are some extra options that can be done for more security.

![Image 24](_project_0ct0pu5_images/image_024.png)
Figure

![Image 25](_project_0ct0pu5_images/image_025.png)
Figure

# Issues Faced while configuring the server

![Image 26](_project_0ct0pu5_images/image_026.png)
Figure : Unable to connect

connection error occured when chaning the password some package were damaged and now not functioning properly this happened because a directory was deleted by mistake and I was able trace and debug the issue by reading the journal of the service that caused the error

![Image 27](_project_0ct0pu5_images/image_027.png)
Figure : Journal log

there was the problem the dashboard was not loading or even working, I tried to unistall it and download it again but the issue was the same the directory was missing

![Image 28](_project_0ct0pu5_images/image_028.png)
Figure : issue solved

the issue is that the directory `/var/ossec/api` without this directory the files of the dashboard can be stored and this will lead to failing the service to start or to make any other action on it. By fixing this everything else went normal.

# Conclusion

This project successfully transformed an old laptop into a centralized Ubuntu-based home network security and monitoring server. By reusing existing hardware and implementing open-source tools, the project provided a low-cost and practical solution for improving home network security, visibility, and control.

Pi-hole was successfully configured to block advertisement and tracking domains across the network, helping to improve privacy and reduce unwanted content. Wazuh was installed as a centralized security monitoring platform, allowing connected devices to send security events and system information to a single dashboard. The successful deployment of a Wazuh agent demonstrated that the server could monitor devices, collect logs, and display security alerts.

![Image 29](_project_0ct0pu5_images/image_029.png)
Figure : Pi-Hole keeps blocking

The project also achieved important network-management objectives, including displaying connected devices, monitoring device availability, blocking selected devices, and restricting internet access after 10 PM through the home router. These features provide greater administrative control and support the planned parental-control function.

Overall, the project met most of its functional requirements and demonstrated that an old laptop can be effectively repurposed as a reliable home network security server. The main remaining task is to implement automatic backups of important configuration files. Future improvements could also include connecting additional devices to Wazuh, refining alert rules, strengthening remote administration, and regularly reviewing Pi-hole blocklists and security logs.

The completed system provides a strong foundation for a more secure, manageable, and observable home network while maintaining low hardware and software costs
