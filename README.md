# Powershell-QuickLine---Quick-Check-Mailbox-MoveRequests-progress

Just copy and paste the below line to launch a periodic check poll (every 10 seconds) of your Mailbox Move requests:

```powershell
while($true){$TimeStampCheck = Get-date;$NextCheck = $TimeStampCheck.AddSeconds(10);$NexStat = get-moverequest
| Get-MoveRequestStatistics;cls;Write-Host "Check:$TimeStampCheck";Write-Host "Next Check : $NextCheck";$NexStat | ft Di
splayName, StatusDetail,TotalMailboxSize, PercentComplete -a;write-host "Seconds before new refresh: " -nonewline;For ($
i=10;$i -ge 0;$i--){Write-Host "$i" -ForegroundColor green -nonewline;if ($i -eq 9){write-host "`b`b "-nonewline}else{wr
ite-host "`b" -nonewline};Sleep 1}}
```
