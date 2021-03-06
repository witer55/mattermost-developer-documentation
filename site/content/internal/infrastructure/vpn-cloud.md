---
title: "VPN(CLOUD)"
date: 2018-06-05T16:08:19+02:00
subsection: internal
weight: 20
---

Table of contents
- [Setup VPN access on Pritunl](#setup-vpn-access-on-pritunl)
  - [Viscosity client](#viscosity-client)
  - [Pritunl client](#pritunl-client)
- [Older Setup of VPN access on OpenVPN](#older-setup-of-vpn-access-on-openvpn)

## Setup VPN access on Pritunl

### Viscosity client   
1. Install a VPN client that supports DNS settings such as Visocity.

```bash
brew cask install viscosity
```

2. Go to the [VPN server](https://pritunl.core.cloud.mattermost.com) and select **Sign in with OneLogin**. 
Then connect with your OneLogin username and password and when prompt put the OTP (One Time Password).
Select `Show More` and hit `Download Profile` 
<span style="display:block;text-align:center;width:40%">![Pritunl User Profiles](/img/vpn_cloud_4.png)</span>


3. Open the Viscosity application or your preferred VPN client and go to settings/preferences.
   
4. Click + to import the profile you downloaded from the VPN server on the step 1
    <span style="display:block;text-align:center;width:50%">![Viscosity Profile Add](/img/vpn_cloud_2.png)</span>

5. After your profile is imported, select to edit the entry, 

- On the General tab update the Address of the Remote Server to be: `pritunl.core.cloud.mattermost.com` as shown below:
   <span style="display:block;text-align:center;width:50%">![General settings Viscosity](/img/vpn_cloud_5.jpg)</span>

- Go to Networking tab and update the DNS settings. 
   * Select for the Mode to be `Split DNS`.  
   * As `Servers` put: `pritunl.core.cloud.mattermost.com` which is VPN's server IP.
   * In `Domains` put: `cloud.mattermost.com`, this will split traffic for those domains
    <span style="display:block;text-align:center;width:50%">![Network settings Viscosity](/img/vpn_cloud_6.jpg)</span>

6. After following these steps you should be able to connect to VPN and then to resolve private DNS entries.


### Pritunl client   
1. Go to the [VPN server](https://pritunl.core.cloud.mattermost.com) and select **Sign in with OneLogin** 
Then connect with your OneLogin username and password and when prompt put the OTP (One Time Password).

2. Select `Download Client` which will redirect you to download the Pritunl Client. 

    Select your OS, download and install the appropriate client.
<span style="display:block;text-align:center;width:40%">![Pritunl Download Client](/img/vpn_cloud_7.jpg)</span>

1. Go back to browser and copy the `Profile URI link`
<span style="display:block;text-align:center;width:40%">![Pritunl Download Client](/img/vpn_cloud_8.jpg)</span>

4. Open the Pritunl client and paste the `Profile URI link` from previous step
   into `Import Profile URI`
   <span style="display:block;text-align:center;width:40%">![Pritunl import URI](/img/vpn_cloud_9.jpg)</span>

   
5. Click the burger button on the newly imported profile and select `Edit Config` 
    <span style="display:block;text-align:center;width:40%">![Pritunl Config](/img/vpn_cloud_10.jpg)</span>

6. On the config change the line that says:
 
    `remote X.XXX.XXX.XX 1194 UDP` to be:

    `remote pritunl.core.cloud.mattermost.com 1194 UDP`
 
    **NOTE:** Do NOT change the port, it will be either 1194, 1195 or something else
   <span style="display:block;text-align:center;width:50%">![Pritunl Config remote](/img/vpn_cloud_11.jpg)</span>

7. After following these steps you should be able to connect to VPN and then to resolve private DNS entries.


## Older Setup of VPN access on OpenVPN


1. Login to the [VPN server](https://vpn.cloud.mattermost.com) using your mattermost email and OneLogin password. Please select `connect` instead of `login` on the drop down menu. 
   * If login fails, ask Cloud team to check if your username is in the correct group
   
2. Please refresh the page if it says:  *Please click here to continue to download OpenVPN Connect.
You will be automatically connected after the installation has finished.*

3. Download the user-locked profile.
    <span style="display:block;text-align:center">![VPN HomePage](/img/vpn_cloud_1.png)</span>

4. Install a VPN client that supports DNS settings such as Visocity.

```bash
brew cask install viscosity
```

5. Open the Viscosity application or your preferred VPN client and go to settings/preferences.
   
6. Click + to import the profile you downloaded from the VPN server on the step 1
    <span style="display:block;text-align:center">![Viscosity Profile Add](/img/vpn_cloud_2.png)</span>

7. After your profile is imported, select to edit the entry, go to Networking tab and update the DNS settings. 
   * Select for the Mode to be `Split DNS`.  
   * As a Server IP put: `10.247.4.47` which is VPN's server IP.
   * In Domains put: `cloud.mattermost.com`, this will split traffic for those domains
    <span style="display:block;text-align:center">![Viscosity VPN CIDR](/img/vpn_cloud_3_new.png)</span>

8. After following these steps you should be able to connect to VPN and then to resolve private DNS entries.
