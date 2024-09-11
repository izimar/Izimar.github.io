---
layout: default
---

# Setting up SSH on an Azure Windows VM and Detecting Successful Login Attempts Using Azure Sentinel

## Objective

This project involves configuring SSH access on a Windows Virtual Machine hosted on Azure and integrating it with Azure Sentinel for monitoring and detecting suceessful login attempts.
---
<p> <br> </p>

### These are the commands used on Azure CLI to properly configure SSH on a Windows machine
<ul class="no-bullets">
<li> [ ~ ]$ myResourceGroup=Izimar_Group </li>
<li> [ ~ ]$ myVM=IzimarVM </li>
<li> [ ~ ]$ az vm extension set --resource-group $myResourceGroup --vm-name $myVM --name WindowsOpenSSH --publisher Microsoft.Azure.OpenSSH --version 3.0 </li>
</ul>


<p> <br> </p>

My resource group variable needed an underscore due to the value containing a space.
If you run into this issue, make sure the value of the variable has an underscore in place of
the space. If your resource group name is "My Resource", then your variable declaration will
look like this in bash: myResourceGroup=My_Variable

---
<p> <br> </p>

### This screenshot shows OpenSSH being successfully added to IzimarVM machine
![test](SSH_Configured.png)

---
<p> <br> </p>

### Created SSH Rule in firewall to allow SSH login from my home IP
![](SSH_FWrule.png)

---
<p> <br> </p>

### This screenshot shows a successful SSH connection to IzimarVM
![](SSH_Connection.png)

---
<p> <br> </p>

### Created rule to alert when SSH in used to access machine
![](Successful_SSH_Rule.png)

---
<p> <br> </p>

### This screenshot shows the incident created from my sucessful SSH login
![](SSH_Incident.png)

---
<p> <br> </p>

## Defense and Hardening

RDP is a commonly used protocol for accessing machines remotely. A good way to harden a device against unauthorized access would be to only allow white listed IPs to access a machine via RDP.
<p> <br> </p>
In this screenshot, the updated RDP rule only allows RDP access from one IP address to any device in the network.
![](HardenedRDP.png)


Still, there are several instances where this hardening technique will not be so effective:
1. A machine with a white listed IP address becomes compromised, bypassing our Firewall rule.
2. A motivated attacker uses IP spoofing to impersonate a white listed IP address.
<p> <br> </p>
In these cases, it would be ideal to have an EDR solution on the target machine to monitor the activity of any users that access the device. As always, having a strong password is a great way to deter bad actors.

---
<p> <br> </p>

## Outcome

The project successfully implemented a robust monitoring solution for RDP logins using Azure Sentinel in the home lab environment. The created alerts provide real-time visibility into RDP access activities, allowing for prompt detection of potential unauthorized access and enhancing overall security posture. This setup not only improves monitoring capabilities but also serves as a practical demonstration of cloud-native security tools.
<p> <br> </p>


[back](./)
<p> <br> </p>
<p> <br> </p>

