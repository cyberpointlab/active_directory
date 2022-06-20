# 01. Installing Domain Controller

1. Use ```sconfig``` to:
    - change the hostname
    - change the IP address to static
    - change the DNS to our own IP addr

2. Install Active Directive Windows Feature

```shell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
```



