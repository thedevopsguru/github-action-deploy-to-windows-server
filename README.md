# github-action-deploy-to-windows-server


add it in your windows server
winrm s winrm/config/client '@{TrustedHosts="13.49.231.50"}'

# Enable PowerShell remoting and WinRM (EC2AMAZ-S7KK8KC -give ur machine name)
Enable-PSRemoting -Force
Set-Item -Path WSMan:\localhost\Client\TrustedHosts -Value EC2AMAZ-S7KK8KC -Force

# Install WinRM dependencies
Install-WindowsFeature -Name "Web-Server" -IncludeManagementTools
Install-WindowsFeature -Name "Web-Mgmt-Service"

# Install WinRM
Install-Module -Name PSWindowsUpdate
Install-Module -Name PowerShellGet
Install-Module -Name PackageManagement
Install-Package -Name "Microsoft.WSMan.Management" -Force

# Configure WinRM
Set-Item -Path WSMan:\localhost\Service\Auth\Basic -Value $true
Set-Item -Path WSMan:\localhost\Service\Auth\Digest -Value $true
Set-Item -Path WSMan:\localhost\Service\AllowUnencrypted -Value $true
Set-Item -Path WSMan:\localhost\Service\MaxEnvelopeSizekb -Value 15360
winrm quickconfig -quiet



====Dummy====
# Check if the WinRM service is running on the remote server
Get-Service -ComputerName EC2AMAZ-S7KK8KC -Name WinRM

# If the service is not running, start it
Start-Service -ComputerName EC2AMAZ-S7KK8KC -Name WinRM


# Check if the remote server is responding to requests
Test-WSMan -ComputerName EC2AMAZ-S7KK8KC


# Test the credentials being used to connect to the remote server
xmDVC?&h@4bXen)C3E.&f&Ap9ZvnIbU9
$credential = "xmDVC?&h@4bXen)C3E.&f&Ap9ZvnIbU9"
Test-WSMan -ComputerName EC2AMAZ-S7KK8KC -Credential "xmDVC?&h@4bXen)C3E.&f&Ap9ZvnIbU9"


# Check the event logs on the remote server for any errors related to WinRM
Get-EventLog -ComputerName EC2AMAZ-S7KK8KC -LogName System -Source "WinRM"


# Run the winrm quickconfig command on the remote server
Invoke-Command -ComputerName EC2AMAZ-S7KK8KC -ScriptBlock {winrm quickconfig}
