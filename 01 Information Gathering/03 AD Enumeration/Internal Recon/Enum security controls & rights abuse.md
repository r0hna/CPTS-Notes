# Disable antivirus
#disableantivirus #antivirusdisable #protectionenum #antivirusenum #security #windowssecurity #disablefirefwall
```
Set-MpPreference -DisableRealtimeMonitoring $true; Set-MpPreference -DisableBehaviorMonitoring $true; Set-MpPreference -DisableBlockAtFirstSeen $true; Set-MpPreference -DisableIOAVProtection $true; Set-MpPreference -DisablePrivacyMode $true; Set-MpPreference -SignatureDisableUpdateOnStartupWithoutEngine $true
```
#### Power-Shell language mode check 
```
$ExecutionContext.SessionState.LanguageMode
```
#### Check windows defender status
```
Get-MpComputerStatus
```
#### List AppLocker rules
```
Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections
```
#### Test `appLocker` policy
```
Get-AppLockerPolicy -Local | Test-AppLockerPolicy -path C:\Windows\System32\cmd.exe -User Everyone

```


---
#### Find LAPS `DelegatedGroups` 
> This right gives the account the ability to read passwords (which domain user can read the LAPS password.)
```
Find-LAPSDelegatedGroups 
```

#### Find `AdmPwdExtendedRights`
>The `Find-AdmPwdExtendedRights` checks the rights on each computer with LAPS enabled for any groups with read access and users with "All Extended Rights." Users with "All Extended Rights" can read LAPS passwords and may be less protected than users in delegated groups, so this is worth checking for.
```
 Find-AdmPwdExtendedRights
```
#### Check LAPS enabled computers 
>We can use the `Get-LAPSComputers` function to search for computers that have LAPS enabled when passwords expire, and even the randomized passwords in clear text if our user has access.
```
Get-LAPSComputers
```

