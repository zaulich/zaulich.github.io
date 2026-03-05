+++
title = "Enable External File Sharing in Teams Chats"
date = 2026-03-05
description = "Allow file sharing in Teams chats with external users using Set-CsTeamsFilesPolicy."
+++

## Quick description

Ever been in a Teams chat with someone from another tenant and hit the classic moment:

*"Can you just email the file instead?"*

Yeah… let's not do that.

With one small policy change, Teams can happily share files directly in chats with external users. No Outlook detours required.

---

## What does this change?

This updates the **Teams Files Policy** (in this case the `Global` policy) to allow **file sharing in chats that include external participants**.

In other words:

If someone from another tenant joins a Teams chat with you, you can drop files directly in the conversation — just like you would with internal users.

---

## What can you do afterwards?

Once enabled, you can:

- Share files directly in **1:1 chats with external users**
- Share files in **group chats that include external participants**
- Collaborate faster with **partners, vendors, and consultants**
- Avoid the dreaded **"I'll just email it instead"** workflow

Basically: Teams chats start behaving like you always expected them to.

---

## What might affect whether it works?

Turning on the policy is only one piece of the puzzle. A few other settings can influence whether file sharing actually works.

Things to check if it doesn't behave as expected:

- **External Access in Teams**  
  If external access is disabled, users from other tenants can't properly participate in chats.

- **SharePoint / OneDrive external sharing settings**  
  Files shared in chat are actually stored in **OneDrive** behind the scenes.  
  If external sharing is restricted there, the upload or share might fail.

- **Sensitivity Labels / Microsoft Purview**  
  Labels or DLP policies may block external sharing depending on classification.

- **Conditional Access policies**  
  Device requirements or session restrictions might affect file access.

- **Client caching / policy propagation**  
  Policy changes can take a little while to propagate. Sometimes a Teams restart helps.

---

## PowerShell

Below is the quickest way to enable the setting.

```powershell
# ------------------------------------------------------------
# Rights required
# ------------------------------------------------------------
# Teams Service Administrator
# Global Administrator
# or equivalent role with permission to manage Teams policies

# ------------------------------------------------------------
# Connect to Microsoft Teams
# ------------------------------------------------------------
Connect-MicrosoftTeams

# ------------------------------------------------------------
# Enable file sharing with external users in chats
# ------------------------------------------------------------
# This updates the Global Teams Files Policy so users
# can share files in chats that include external participants.

Set-CsTeamsFilesPolicy `
    -Identity Global `
    -FileSharingInChatsWithExternalUsers Enabled

# ------------------------------------------------------------
# Verify the configuration
# ------------------------------------------------------------
# This confirms the policy setting is enabled.

Get-CsTeamsFilesPolicy -Identity Global |
Select-Object Identity, FileSharingInChatsWithExternalUsers

# Expected output:
#
# Identity   FileSharingInChatsWithExternalUsers
# --------   -----------------------------------
# Global     Enabled
```

---

## Final thoughts

Sometimes the difference between *"This collaboration is easy"* and  
*"Can you just email the file?"*  

…is literally one PowerShell command.

Flip the switch, keep the conversation in Teams, and let files travel across tenants the way they probably should have all along.