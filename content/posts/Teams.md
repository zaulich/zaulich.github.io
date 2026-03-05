+++
title = "Enable External File Sharing in Teams Chats"
date = 2026-03-05
description = "Use Set-CsTeamsFilesPolicy to allow file sharing with external users in chat."
+++

Sometimes you just need to toss a spreadsheet across tenant borders without the awkward  
"Could you email it instead?" follow-up.

Microsoft Teams can actually handle this just fine — you just need to flip the right switch.

---

## The Magic One-Liner

```powershell
Set-CsTeamsFilesPolicy -Identity Global -FileSharingInChatsWithExternalUsers Enabled
```

Simple as that.

One command and suddenly your chat participants outside the tenant can receive files directly in the conversation.  
No email gymnastics required.

---

## What This Actually Does

> This updates the **Global Teams Files Policy** and allows files to be shared in chats that include external participants.

So if you're chatting with:

- partners  
- vendors  
- consultants  
- that one freelancer who somehow lives in three different tenants  

…they can now receive files directly in the Teams chat.

---

## Before You Run It

A couple of quick checks before you unleash file-sharing greatness:

- You must be connected to **Microsoft Teams PowerShell**
- You need **Teams Service Admin** (or higher)
- **External Access must be enabled** in Teams

If external access is disabled, Teams will still refuse to play nice.

---

## Verify the Setting

```powershell
Get-CsTeamsFilesPolicy -Identity Global |
Select-Object Identity, FileSharingInChatsWithExternalUsers
```

Expected output:

```
Identity   FileSharingInChatsWithExternalUsers
--------   -----------------------------------
Global     Enabled
```

If you see **Enabled**, you're good to go.

---

## Final Thoughts

Sometimes the simplest fixes are just hidden behind obscure PowerShell parameters.

Now you can send files across tenants directly in Teams — without switching to Outlook like it's 2007.

Your partners will thank you.  
Your inbox will thank you.  
And somewhere, a spreadsheet will travel freely between tenants.