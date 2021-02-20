---
layout: post
title:  "Get Device Hardware Hash ID with PowerShell Script"
date:   2021-02-05 14:55:31 +0000
categories: tech, PowerShell, Autopilot, InTune
image: /assets/img/autopilot.png
---
Not sure how many people are actually grabbing hardware hash id manually, but I am doing it because sometimes clients are not requesting it when buying the devices in bulk. So, if you will also be in the same position as me, this is how you can get hash id, save it to usb and upload to the InTune for autopilot process.

<img src="{{ page.image }}">
<br><br>
When you buy devices in bulk, they should already have Windows 10 Pro on them so just start the device and wait until you get some kind of screen. Usually something like windows asking for language and keyboard leyout.
Next step is to press Shift + F10 or FN + Shift + F10 and that will give you CMD terminal. This is where you need to start the PowerShell and type a few commands as seen on the Microsoft page <a href="https://docs.microsoft.com/en-us/mem/autopilot/add-devices">https://docs.microsoft.com/en-us/mem/autopilot/add-devices </a>

Also, connect the USB drive where you want to copy the CSV file.


{% highlight ruby %}
PS
New-Item -Type Directory -Path "C:\HWID"
Set-Location -Path "C:\HWID"
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted
Install-Script -Name Get-WindowsAutoPilotInfo
Get-WindowsAutoPilotInfo.ps1 -OutputFile AutoPilotHWID.csv
Copy-Item "C:\HWID\AutoPilotHWID.csv" -Destination "D:\"
{% endhighlight %}

Now you can already see that we can make some kind of shortcut to those commands so this is what I use:

{% highlight ruby %}
PS
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted
Install-Script -Name Get-WindowsAutoPilotInfo
Get-WindowsAutoPilotInfo.ps1 -OutputFile "D:\AutoPilotHWID.csv"
{% endhighlight %}

Now this file can be used to import device with its hash id to InTune.
If you want to know more about the script, please visit <a href="https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo/3.5">https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo/3.5</a>