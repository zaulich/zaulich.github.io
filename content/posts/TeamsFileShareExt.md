+++
title = "Enable External File Sharing in Teams Chats"
date = 2026-03-05
description = "Allow file sharing in Teams chats with external users using Set-CsTeamsFilesPolicy."
[taxonomies]
tags=["Teams","PowerShell"]
+++
{% tldr() %}
**Don't want the long explanation?**

Run this:
```powershell
Connect-MicrosoftTeams
Set-CsTeamsFilesPolicy -Identity Global -FileSharingInChatsWithExternalUsers Enabled
{% end %}

------------------------------------------------------------------------

## The problem
<img src="/images/doh.gif" 
     style="float:right;width:260px;margin:0 0 1rem 1.5rem;border-radius:6px;">
You've probably seen this before.

You're chatting with someone from another tenant in Teams and want to
share a file.

Then Teams politely tells you <span class="big-no">NO</span>.


So the conversation quickly becomes:

> "Can you just email the file instead?"

Which is exactly the kind of workflow Teams was supposed to replace.
<div style="clear: both;"></div>

------------------------------------------------------------------------

## The fix

Teams actually supports file sharing in chats with external users --- it
just isn't always enabled.

By updating the **Teams Files Policy**, you allow users to drop files
directly into chats that include people from other tenants.

After enabling this setting, users can:

-   Share files in **1:1 chats with external users**
-   Share files in **group chats with external participants**
-   Collaborate without falling back to email

Exactly how chat collaboration should work.

------------------------------------------------------------------------

## PowerShell

All it takes is one setting.

``` powershell
# Requires:
# Teams Service Administrator or Global Administrator

Connect-MicrosoftTeams

Set-CsTeamsFilesPolicy `
    -Identity Global `
    -FileSharingInChatsWithExternalUsers Enabled
```

Optional sanity check:

``` powershell
Get-CsTeamsFilesPolicy -Identity Global |
Select Identity, FileSharingInChatsWithExternalUsers
```

------------------------------------------------------------------------

## If it still doesn't work

This setting is only one piece of the puzzle. File sharing can still be
affected by:

-   **External Access in Teams**
-   **OneDrive / SharePoint external sharing settings**
-   **Sensitivity labels or DLP policies**
-   **Conditional Access restrictions**

But in most environments, enabling this policy is the missing piece.

------------------------------------------------------------------------

## Final thought

Sometimes improving collaboration across tenants sounds like a big
project.

Sometimes it's just:

``` powershell
Set-CsTeamsFilesPolicy -Identity Global -FileSharingInChatsWithExternalUsers Enabled
```

And suddenly nobody has to say\
*"I'll just email it instead."*
