# escape=`
FROM microsoft/aspnet:windowsservercore-10.0.14393.1593

COPY UpgradeSample-1.0.0.0.msi C:\

RUN msiexec /i C:\UpgradeSample-1.0.0.0.msi RELEASENAME=2017.10 /qn