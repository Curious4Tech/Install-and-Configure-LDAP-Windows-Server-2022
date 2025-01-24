# Install-and-Configure-LDAP-Windows-Server-2022
A comprehensive guide to installing and configuring Lightweight Directory Access Protocol (LDAP) on a Windows Server 2022 domain controller using the GUI. Includes steps for setting up Active Directory, enabling LDAP over SSL, verifying configurations, and testing access. Perfect for administrators and IT professionals.

# Install and Configure LDAP on Windows Server 2022 Using GUI

This guide outlines how to install and configure Lightweight Directory Access Protocol (LDAP) on a Windows Server 2022 domain controller using the graphical user interface (GUI).

## Prerequisites
- A Windows Server 2022 system configured as a domain controller.
- Administrator access to the server.
- Active Directory Certificate Services (AD CS) installed and configured.

---

## Step 1: Confirm Active Directory is Installed
LDAP is part of Active Directory Domain Services (AD DS). Ensure AD DS is installed and the server is configured as a domain controller.

1. Open **Server Manager**.
2. Verify that the **Active Directory Domain Services** role is installed.
3. Verify that the **Active Directory Certificate Services (AD CS)** is  installed and configured


![image](https://github.com/user-attachments/assets/d890799d-65ae-4798-b2ac-ea7cd434664e)

---

## Step 2: Install Additional Features (If Necessary)

1. Open **Server Manager**.
2. Click **Add roles and features**.
3. Proceed through the wizard:
   - On the **Server Roles** page, ensure **Active Directory Domain Services** is selected.
   - On the **Features** page, ensure the following features are installed:
     - **Group Policy Management**
     - **RSAT: Active Directory Administration Center**
     - **RSAT: Active Directory Users and Computers**
4. Complete the wizard and install missing features, if necessary.

---

## Step 3: Enable LDAP Over SSL (Optional but Recommended)

To enable secure LDAP (LDAPS):

1. **Obtain or create an SSL/TLS certificate** for the domain controller:
   - **Use a Certificate Authority (CA):** Request a certificate from an internal or external CA that includes the Fully Qualified Domain Name (FQDN) of the domain controller.
     - Open **Server Manager**.
     - Go to **Tools > Certification Authority**.

![image](https://github.com/user-attachments/assets/b037819d-8b2d-40c6-8c6e-9ae74d40d822)

   - You should see an issued certificate for the domain controller.

![image](https://github.com/user-attachments/assets/67caf1bb-1b34-4124-9d4b-eacc5d6be295)

     
2. **Install the certificate:**
   - Open **Run (Win + R)**, type `mmc`, and press **Enter**.

![image](https://github.com/user-attachments/assets/50d17eb5-dc82-454f-a836-83d2c188109d)

   - In the MMC console, go to **File > Add/Remove Snap-in**.

![image](https://github.com/user-attachments/assets/81759d8a-cfaf-430e-a216-a5528a737b2d)

   - Double-click on **Certificates**

![image](https://github.com/user-attachments/assets/d0984fd9-4d13-4b3d-9a36-5a3e67f6cedf)

   - choose **Computer account** and click **Next**.
   - 
![image](https://github.com/user-attachments/assets/e4e5890b-e713-4eab-b14a-d920ea204b13)

   - Select **Local Computer** and click **Finish**.

![image](https://github.com/user-attachments/assets/c85eaaa0-9d2d-4fd5-9784-247c4135af6e)

   - Navigate to **Certificates (Local Computer) > Personal > Certificates**.

![image](https://github.com/user-attachments/assets/c989ba2e-5408-448c-b8ff-62812525b707)

   -If certificates aren't already installed, you'll need to import them by right-clicking the **Personal** folder, choose **All Tasks > Import**, and follow the wizard to import the certificates.

![image](https://github.com/user-attachments/assets/d9e46744-4ed7-4f5a-96cf-f4cb7b1386e1)

2. **Restart the Active Directory Domain Services service:**
   - Open **Run (Win + R)**, type `services.msc`, and press **Enter**.
   - Locate **Active Directory Domain Services** in the list.
   
![image](https://github.com/user-attachments/assets/b05b3fda-6689-420c-8ff6-aa0d7ef9dbb1)

   - Right-click and select **Restart**.

![image](https://github.com/user-attachments/assets/670c4ba3-43f8-4e53-b393-e32ec6191fe9)

---

## Step 4: Configure LDAP Settings

### Verify LDAP Functionality

1. Open **Active Directory Users and Computers**.
2. Use LDAP queries to search for objects in the domain:
   - Right-click the domain root and select **Find**.
   - Use **Custom Search** or **LDAP Query**.

![image](https://github.com/user-attachments/assets/7e88e44e-128a-4acf-a08d-63b67323c7fe)

### Test the LDAP Connection

1. Open **LDP.exe** (Run `ldp.exe`).
2. Connect to the domain controller:
   - Use the FQDN of the domain controller.
   - Use port **389** for LDAP or **636** for LDAPS.

![image](https://github.com/user-attachments/assets/6e1716df-209b-480e-8fc4-9dafc1481ea9)

3. Successifully connected

![image](https://github.com/user-attachments/assets/0a7b6319-3da6-4a24-a918-72464827c54b)

4. Bind using domain credentials.

![image](https://github.com/user-attachments/assets/c5ae6751-1217-4a61-88d0-9e1302ba9492)


---

## Step 5: Verify Ports and Firewall

Ensure the required ports are open:

| Protocol  | Port | Purpose        |
|-----------|------|----------------|
| TCP       | 389  | LDAP           |
| TCP       | 636  | LDAP over SSL  |

### Configure Firewall Rules

1. Open **Windows Defender Firewall**.
2. Go to **Advanced Settings**.
3. Add inbound rules for ports **389** and **636**, if not already present.

---

## Step 6: Test LDAP Access

Use an LDAP client to test access:

- **LDP.exe** (built into Windows).
- Third-party tools like **Softerra LDAP Browser** or **Apache Directory Studio**.

---

## Notes
- LDAP is inherently part of Active Directory. No additional installation is needed if AD DS is configured.
- To customize schemas or organizational units, use **Active Directory Users and Computers**.

---

## Resources
- [Microsoft Docs: Active Directory LDAP](https://docs.microsoft.com/en-us/windows-server/identity/ldap/)
- [Active Directory Administration Tools](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/manage/active-directory-administration-tools)
