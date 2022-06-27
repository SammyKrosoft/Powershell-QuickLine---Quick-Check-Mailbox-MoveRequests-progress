# Powershell-Quickie: Quick Mailbox MoveRequests realtime monitoring console one-liner


***Prerequisite** : The below one-liner PowerShell line has to be pasted on a PowerShell console with Exchange Management Tools loaded (either Exchange Online or Exchange 2016/2019/2022).*

Here is a single PowerShell command line, actually several instructions separated by semicolons, to run a sort of realtime monitoring console that shows all your Move Requests in progress, refreshed every 10 seconds (or choose the number of seconds you want for each refresh).

On an Exchange Management Shell console (aka a Powershell session in which you have Exchange management cmdlets loaded), just copy and paste the below one-liner PowerShell instructions to launch a periodic check poll (every 10 seconds) of your Mailbox Move requests:

```powershell
while($true){$TimeStampCheck = Get-date;$NextCheck = $TimeStampCheck.AddSeconds(10);$NexStat = get-moverequest | Get-MoveRequestStatis
tics;cls;Write-Host "Check:$TimeStampCheck";Write-Host "Next Check : $NextCheck";$NexStat | ft DisplayName, PercentComplete, SourceDatabase, Ta
rgetDatabase, TotalMailboxSize, StatusDetail -a;write-host "Seconds before new refresh: " -nonewline;For ($i=10;$i -ge 0;$i--){Write-Host "$i"
-ForegroundColor green -nonewline;if ($i -eq 9){write-host "`b`b "-nonewline}else{write-host "`b" -nonewline};Sleep 1}}
```

The above command line will poll forever the Exchange Move Requests status every 10 seconds, until you interrupt the loop (CTRL+C). You can for example run the above line in a PowerShell session (with Exchange Management Tools loaded) in the background or on another screen with other monitoring stuff, and manage your migration requests and migration batches on another PowerShell session, and you'll see the output evolve in realtime (refreshed every 10 seconds).

The output will look like the below and will run forever, with a refresh every 10 seconds, until you interrupt the process with CTRL+C or by simply closing the Powershell console:

![image](https://user-images.githubusercontent.com/33433229/176021663-5f0e90b3-cfa3-4fcd-9d49-fa4dc63bc43d.png)
