# Install-and-Configure-LDAP-Windows-Server-2022
A comprehensive guide to installing and configuring Lightweight Directory Access Protocol (LDAP) on a Windows Server 2022 domain controller using the GUI. Includes steps for setting up Active Directory, enabling LDAP over SSL, verifying configurations, and testing access. Perfect for administrators and IT professionals.

# Install and Configure LDAP on Windows Server 2022 Using GUI

This guide outlines how to install and configure Lightweight Directory Access Protocol (LDAP) on a Windows Server 2022 domain controller using the graphical user interface (GUI).

## Prerequisites
- A Windows Server 2022 system configured as a domain controller.
- Administrator access to the server.

---

## Step 1: Confirm Active Directory is Installed
LDAP is part of Active Directory Domain Services (AD DS). Ensure AD DS is installed and the server is configured as a domain controller.

1. Open **Server Manager**.
2. Verify that the **Active Directory Domain Services** role is installed.

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
   - Use a Certificate Authority (CA) or create a self-signed certificate.
   - Ensure the certificate includes the Fully Qualified Domain Name (FQDN) of the domain controller.

2. Install the certificate:
   - Open **Certificates (Local Computer)** via the MMC console.
   - Import the certificate into the **Personal** store.

3. Restart the **Active Directory Domain Services** service:
   - Open **Services** from the Start menu.
   - Locate and restart the **Active Directory Domain Services** service.

---

## Step 4: Configure LDAP Settings

### Verify LDAP Functionality

1. Open **Active Directory Users and Computers**.
2. Use LDAP queries to search for objects in the domain:
   - Right-click the domain root and select **Find**.
   - Use **Custom Search** or **LDAP Query**.

### Test the LDAP Connection

1. Open **LDP.exe** (Run `ldp.exe`).
2. Connect to the domain controller:
   - Use the FQDN of the domain controller.
   - Use port **389** for LDAP or **636** for LDAPS.
3. Bind using domain credentials.

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

