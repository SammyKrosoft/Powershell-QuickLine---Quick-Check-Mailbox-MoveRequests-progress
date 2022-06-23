# Powershell-QuickLine---Quick-Check-Mailbox-MoveRequests-progress

On an Exchange Management Shell console (aka a Powershell session in which you have Exchange management cmdlets loaded), just copy and paste the below one-liner PowerShell instructions to launch a periodic check poll (every 10 seconds) of your Mailbox Move requests:

```powershell
while($true){$TimeStampCheck = Get-date;$NextCheck = $TimeStampCheck.AddSeconds(10);$NexStat = get-moverequest | Get-MoveRequestStatis
tics;cls;Write-Host "Check:$TimeStampCheck";Write-Host "Next Check : $NextCheck";$NexStat | ft DisplayName, PercentComplete, SourceDatabase, Ta
rgetDatabase, TotalMailboxSize, StatusDetail -a;write-host "Seconds before new refresh: " -nonewline;For ($i=10;$i -ge 0;$i--){Write-Host "$i"
-ForegroundColor green -nonewline;if ($i -eq 9){write-host "`b`b "-nonewline}else{write-host "`b" -nonewline};Sleep 1}}
```

The output will look like the below:

![image](https://user-images.githubusercontent.com/33433229/175197268-3e3709be-ab6a-4d60-abf9-d3f5d32521bf.png)
