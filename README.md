# Remote PowerShell Commands

## Lab Mission
Manage a client Windows 10 environment remotely from the Windows 2016 Server via PowerShell.


## Requirements
- Familiarity with Active Directory domain services
- Understanding of network services
- Experience with server-client environments
- Knowledge of PowerShell commands

## Resources
**Environment and Tools:**
- VirtualBox:
  - Windows Server 2016 (Server1)
  - Windows 10 Client

---

## Lab Task: Execute Remote PowerShell Commands
Manage a client machine from the **Server1** machine by using remote PowerShell commands.

1. Log in to the Windows 10 client and open PowerShell as an administrator. Enable remote PowerShell commands by using:
   `Enable-PSRemoting -force`

2. Use `ping 10.0.0.1` to verify connectivity to the server.

3. Start the **Windows Remote Management** service for the next step to work. In the Windows search bar, enter `services.msc`, then find **Windows Remote Management** and click the green start button.

4. On **Server1**, open PowerShell as an administrator. Use the following command to show the remote computer’s name:
   `Invoke-Command -ComputerName Client10 -Credential Cyber\administrator -ScriptBlock {hostname}`
   *Tip: If you are already logged in with an administrator account, you don’t have to use the `-Credential` parameter.*

5. Use `Invoke-Command` as follows to create a local user on the remote client:
   `Invoke-Command -ComputerName Client10 -Credential Cyber\Administrator -ScriptBlock {net user invoke_user ‘(Secure Password)’ /add}`

6. Verify the new user was created on the remote client machine by using the following:
   `Invoke-Command -ComputerName Client10 -Credential Cyber\administrator -ScriptBlock {net user}`

7. Start a session between the server and client machines by using the `Enter-PSSession` command. Enter the correct computer name (**Client10**).

8. Verify that the server is remotely logged in to the client machine using the `hostname` command.

9. Remotely check the client machine’s IP by using the `ipconfig` command.

10. Use `Get-Process` to show the client process (you can also start and stop a process).

11. Create a directory on the desktop by using:
    `cd C:\Users\administrator\Desktop` and `mkdir Test_File`

12. Verify the directory was created through PowerShell by using the `dir` command.

13. Restart the client computer remotely by using:
    `Restart-Computer -force`
