---
tags:
  - self-hosted
  - github-actions-runner
---


This guide shows you how to change the account under which your GitHub Actions self-hosted runner service runs. By default, the service may run under a restricted account. Changing it to a higher-privileged account like **NT AUTHORITY\SYSTEM** can help if you need extra permissions.

## Step 1: Find the Service Name

Open an elevated PowerShell window (Run as Administrator) and run the following command to list the service names of all GitHub Actions runners:

```powershell
(Get-Service actions.runner.*).Name
```

This command will display the service name(s) that match the pattern `actions.runner.*`.

## Step 2: Update the Service Account

Now that you have the service name, run the following command to change the account. Use **sc.exe** (to avoid conflicts with PowerShell aliases):

```powershell
sc.exe config "actions.runner.AldeRoberge-AutomaticDialogGenerator.RNWMONTEUR-2" obj= "NT AUTHORITY\SYSTEM" type= own
```

**Note:**
- Replace `"actions.runner.AldeRoberge-AutomaticDialogGenerator.RNWMONTEUR-2"` with your actual service name if different.
- Ensure there is a space after `obj=`.

## Step 3: Restart the Service

After reconfiguring the service, restart it to apply the changes:

```powershell
Restart-Service "actions.runner.AldeRoberge-AutomaticDialogGenerator.RNWMONTEUR-2"
```

Again, replace the service name if needed.

---

By following these steps, your GitHub Actions runner will run under the **NT AUTHORITY\SYSTEM** account, granting it higher privileges to execute commands as needed.>)