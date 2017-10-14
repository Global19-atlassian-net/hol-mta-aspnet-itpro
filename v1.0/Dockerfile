# escape=`
FROM microsoft/aspnet:windowsservercore-10.0.14393.1593
SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop';"]

COPY UpgradeSample-1.0.0.0.msi C:\

RUN Start-Process msiexec.exe -ArgumentList '/i', 'C:\UpgradeSample-1.0.0.0.msi', 'RELEASENAME=2017.10', '/quiet', '/norestart' -NoNewWindow -Wait