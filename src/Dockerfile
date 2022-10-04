# Dockerfile for Windows Servercore + PHP 5.6 + IIS

FROM chocolatey/choco:latest-windows

RUN choco install php --params "/ThreadSafe /InstallDir:C:\php" --version=5.6.40 --yes
RUN choco install sql2012.nativeclient --yes

# Set environment variables
RUN setx PATH /M %PATH%;C:\php

# Enable WindowsFeature for IIS
RUN powershell -command Add-WindowsFeature Web-Server
RUN powershell -command Add-WindowsFeature Web-CGI

# Setup php config in IIS
COPY .//config/applicationHost.config C://Windows//System32//inetsrv//config//applicationHost.config
COPY .//config/index.php C://inetpub//wwwroot//default//index.php
COPY .//config/web.config C://inetpub//wwwroot//default//web.config
COPY .//php5.6.36-drivers/php_pdo_sqlsrv_56_ts.dll C://php/ext/php_pdo_sqlsrv_56_ts.dll
COPY .//php5.6.36-drivers/php_sqlsrv_56_ts.dll C://php/ext/php_sqlsrv_56_ts.dll
COPY .//config/php.ini C://php/php.ini