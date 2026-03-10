# Azure application vpn security
Demonstration of an end to end  secure internal HRM Application implementation
<img src="https://i.imgur.com/bIY7wTE.png" height="80%" width="80%" />

<h2> Applications and Utilities Used</h2>

- <b>OrangeHRM Human Resources Application</b>
- <b>SSL certification</b>
- <b>Ubuntu Linux</b>
- <b>Vnets, Subnets, VPNgateway, Network Security Groups, VnetPeering</b>
- <b>Bastion</b>
- <b>Blob Storage</b>
- <b>Entra ID</b>
- <b>MFA</b>
- <b>Microsoft Defender</b>
- <b>Microsoft Sentinel</b>
- <b>Windows 10 VPN, AzureVPN client</b>

<h2>Program walk-through:</h2>
This project focused on securing a private HR application hosted on Azure.
The user connects from their laptop/computer via Azure VPN securing the communication
between the web application and the user, additionally i applied  mfa, and a ssl certificate aswell.

The hr web app is secured with windows defender to scan for vulnerabilities and viruses.For sentinel
i applied an analytics rule to notify me of failed logins on the web app.

The infrastructure was built using several Azure networking components:
 - Virtual Networks and Subnets were created to separate application resources from the VPN access network.
 - A VPN Gateway was configured to allow secure Point-to-Site (P2S) connections.
 - A Windows 10 client using the Azure VPN Client connects to the environment and receives an IP address from the VPN address pool.
 - Virtual Network Peering was configured so the VPN network could communicate with the application network.
 - Network Security Groups (NSGs) were used to restrict traffic and allow only the necessary ports (such as HTTPS) to the application VM.
 - Azure Bastion was deployed to securely manage the virtual machines without exposing RDP/SSH directly to the internet.
   
This architecture ensures the HR application is not publicly exposed and is only reachable through the VPN connection.


<h2>Quick Video walk through</h2>
 
<h3>Challenges and constraints</h3>
This lab was built using an Azure free-tier environment, which introduced some limitations that influenced the final implementation.

Some planned security features could not be fully implemented due to licensing restrictions. Features such as Conditional Access Policies, Data Loss Prevention (DLP), and advanced Entra ID application authentication integration require Entra ID Premium (P1/P2) or Microsoft 365 security licensing. Because the lab used a free tenant and trial activation was unavailable for the account, these capabilities could not be enabled.

During the networking setup, there were also several troubleshooting challenges. The most significant issue involved enabling communication between the VPN network and the application network. Initially, VNet peering settings repeatedly failed to apply, preventing the VPN-connected client from reaching the OrangeHRM application.

The issue required several troubleshooting steps, including:
 - Investigating incorrect NAT network settings on the Windows 10 virtual machine used as the VPN client.
 - Verifying route advertisements and address pools from the VPN gateway.
 - Confirming Network Security Group (NSG) rules were not blocking required traffic.
 - Reapplying VNet peering settings, including allowing the application network to use the VPN network’s remote gateway.
 - Once the peering configuration successfully applied, VPN clients were able to reach the internal HRM application.

These constraints and troubleshooting steps reflect common real-world challenges when working with cloud networking, licensing limitations, and identity security features in Azure lab environments.

