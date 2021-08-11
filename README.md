# TIP: Quick script to get your Exchange Servers exact version numbers

```powershell
$ExchangeServers = Get-ExchangeServer | Sort-Object Name
ForEach ($Server in $ExchangeServers) {
    Invoke-Command -ComputerName $Server.Name -ScriptBlock { Get-Command Exsetup.exe | ForEach-Object { $_.FileversionInfo } }
}
```

Sample output (my Lab):

```output
ProductVersion   FileVersion      FileName                            PSComputerName                    
--------------   -----------      --------                            --------------                    
15.01.2044.004   15.01.2044.004   C:\Program Files\Microsoft\Excha... E2016-01                          
15.01.2308.008   15.01.2308.008   C:\Program Files\Microsoft\Excha... E2016-02                          
```

## Compare the versions you get from the above with the numbers on the below link:

## [Exchange build numbers and all CUs download links](https://docs.microsoft.com/en-us/exchange/new-features/build-numbers-and-release-dates?view=exchserver-2019)

Example finding my CU level with the above example:

<img src = https://user-images.githubusercontent.com/33433229/125547107-9a243329-43fc-4435-b32b-8613d5fc1a74.png width = 600>

==> My server E2016-02 is at CU21 without the July 2021 security fix

And the other one (15.01.2044.004):

<img src = "https://user-images.githubusercontent.com/33433229/125547168-b23686d5-9160-4961-ab57-8624369ac27b.png" width = 600>

==> My server E2016-01 is at CU17 (need to update ASAP !)

After updating E2016-01, I can check the versions again:

```output
ProductVersion   FileVersion      FileName                            PSComputerName
--------------   -----------      --------                            --------------
15.01.2308.014   15.01.2308.014   C:\Program Files\Microsoft\Excha... E2016-01
15.01.2308.008   15.01.2308.008   C:\Program Files\Microsoft\Excha... E2016-02
```

=> my E2016-01 server is up to date with Exchange 2016 CU21 + July 2021 security update (note the .014 suffix), and E2016-01 just has CU21 (note the .008 suffix)
