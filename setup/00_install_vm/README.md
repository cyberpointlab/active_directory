# 00 - Install VM


# 1. Install Windows Server 2022 VM
    - ```enable-PSRemoting```
    - Setup server name
    - Setup networking 
        - Static IP addr
        - Default gateway
        - Primary DNS
    ## Install AD
    ```Install-WindowsFeature AD-Domain-Services -IncludeManagementTools```
    ```Import-Module ADDSDeployment```
    ```Install-ADDSForest```
    - Setup DNS again because it is reverted to loopback 127.0.0.1

# 2. Create/Spawn Windows VM - Management workstation

- Add server to ```TrustedHost```
        To enable remote management of a computer or server through WinRM (Windows Remote Management), add computers to the TrustedHosts list. 
        ```shell
           
            ls WSMan:\localhost\Client\TrustedHost\

            Set-Item WSMan:\localhost\Client\TrustedHosts -Value $ip
           
            New-PSSession -ComputerName $ip -Credential (Get-Credential) 

        ```
    - Enter PSSession    
    ```Enter-PSSession $ID```

# 3. Create/Spawn Windows VM - Workstation client
    ## setup networking
    ```Get-NetIpAddress``` //this is to find out interface index
    ```Get-DNSClientServerAddress```
    ```Set-DNSClientServerAddress -InterfaceIndex 10 -ServerAddresses $ip```
 
    ## Join computer to domain
     ```Add-Computer -DomainName $domainname -Credential $domainname\administrator -Force -Restart```
