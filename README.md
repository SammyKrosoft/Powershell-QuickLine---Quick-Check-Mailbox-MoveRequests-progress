# Powershell-Quickie: Quick Mailbox MoveRequests realtime monitoring console

Here is a single PowerShell command line, actually several instructions separated by semicolons, to run a sort of realtime monitoring console that shows all your Move Requests in progress, refreshed every 10 seconds (or choose the number of seconds you want for each refresh).

On an Exchange Management Shell console (aka a Powershell session in which you have Exchange management cmdlets loaded), just copy and paste the below one-liner PowerShell instructions to launch a periodic check poll (every 10 seconds) of your Mailbox Move requests:

```powershell
while($true){$TimeStampCheck = Get-date;$NextCheck = $TimeStampCheck.AddSeconds(10);$NexStat = get-moverequest | Get-MoveRequestStatis
tics;cls;Write-Host "Check:$TimeStampCheck";Write-Host "Next Check : $NextCheck";$NexStat | ft DisplayName, PercentComplete, SourceDatabase, Ta
rgetDatabase, TotalMailboxSize, StatusDetail -a;write-host "Seconds before new refresh: " -nonewline;For ($i=10;$i -ge 0;$i--){Write-Host "$i"
-ForegroundColor green -nonewline;if ($i -eq 9){write-host "`b`b "-nonewline}else{write-host "`b" -nonewline};Sleep 1}}
```

The above command line will poll forever the Exchange Move Requests status every 10 seconds, until you interrupt the loop (CTRL+C). You can for example run the above line in a PowerShell session (with Exchange Management Tools loaded) in the background or on another screen with other monitoring stuff, and manage your migration requests and migration batches on another PowerShell session, and you'll see the output evolve in realtime (refreshed every 10 seconds).

The output will look like the below:

![image](https://user-images.githubusercontent.com/33433229/175197268-3e3709be-ab6a-4d60-abf9-d3f5d32521bf.png)
