# escape=`
FROM microsoft/aspnet:windowsservercore-10.0.14393.1715
SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

RUN Set-WebConfigurationProperty -pspath 'MACHINE/WEBROOT/APPHOST' -filter 'system.applicationHost/log' -name 'centralLogFileMode' -value 'CentralW3C'; `
    Set-WebConfigurationProperty -pspath 'MACHINE/WEBROOT/APPHOST' -filter 'system.applicationHost/log/centralW3CLogFile' -name 'truncateSize' -value 4294967295; `
    Set-WebConfigurationProperty -pspath 'MACHINE/WEBROOT/APPHOST' -filter 'system.applicationHost/log/centralW3CLogFile' -name 'period' -value 'MaxSize'; `
    Set-WebConfigurationProperty -pspath 'MACHINE/WEBROOT/APPHOST' -filter 'system.applicationHost/log/centralW3CLogFile' -name 'directory' -value 'c:\iislog'

ENTRYPOINT ["powershell"]
CMD Start-Service W3SVC; `
    Invoke-WebRequest http://localhost/UpgradeSample -UseBasicParsing | Out-Null; `
    netsh http flush logbuffer | Out-Null; `
    Get-Content -path 'c:\iislog\W3SVC\u_extend1.log' -Tail 1 -Wait

WORKDIR C:\
COPY UpgradeSample-1.1.0.0.msi .
RUN msiexec /i c:\UpgradeSample-1.1.0.0.msi RELEASENAME=2017.11 /qn