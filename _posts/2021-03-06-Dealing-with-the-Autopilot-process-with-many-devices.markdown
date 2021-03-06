---
layout: post
title:  "Dealing with the Autopilot process and many devices"
date:   2021-03-06 17:55:31 +0000
categories: tech, PowerShell, Autopilot, InTune
author: Josip Bognar
image: /assets/img/autopilot2.png
comments: true
---
If you are working in any bigger company, you might have had a chance to work with the Autopilot process or the White glove. One of most important things are to have hash ids for devices or ask for them from the company you are buying your devices from, but if you are unlucky one, you will need to do it manually for maybe thousands of the devices so this is my experience of doing it.

To get device hash id, there are two ways. Doing it manually and saving them to some CSV file or by using script Upload-WindowsAutopilotDeviceInfo, which requires an account with admin privilege.

Script source: [Powershell gallery](https://www.powershellgallery.com/packages/Upload-WindowsAutopilotDeviceInfo/1.1.0)

This process involves a lot of manual typing and if you need to do all those things on each device, it will soon become most tedious part of the job. While watching my colleagues going mad, I have decided to put a bit of effort into making this part of the process smoother by creating one batch file and additional small script to automate the process and get rid of possible typing errors.

<img src="{{ page.image }}">
<br><br>
There are two separate files you will need to create, one is *.bat and another is *.sp1 and you can save them to the USB flash memory stick.

*.bat:
{% highlight ruby %}
powershell.exe -NoProfile -ExecutionPolicy unrestricted -command "& {start-process powershell -argumentlist ' -NoProfile -Executionpolicy unrestricted -file ""D:\name-of-your-script-file.ps1""' -Verb Runas}"
{% endhighlight %}

*.ps1:
{% highlight ruby %}
write-output "Starting script download..."
install-script -name upload-windowsautopilotdeviceinfo
Start-Sleep -Seconds 15
write-output "Starting uploading data..."
$Tag = Read-Host -Prompt 'Input GroupTag ID'
write-output "Connecting to Azure Tenant, soon you will need to enter your details ..."
upload-windowsautopilotdeviceinfo.ps1 -TenantName "tenant.onmicrosoft.com" -GroupTag "$Tag" -verbose
write-output "going to sleep mode - Finished"
Start-Sleep -Seconds 60
{% endhighlight %}

After you save the files, plug-in the USB stick to the device, and at the language selection stage open the CMD(usually Shift + F10 or FN + Shift + F10) and type command:

Start D:\your-batch-file-name.bat

This will than do all the process for you with addition to asking you a few question about the execution policy, the script installation and the GroupTag. If you are new to the Autopilot process, please find doc's on this link [Powershell gallery](https://docs.microsoft.com/en-us/mem/autopilot/)

Hope this will help someone if they get into the bad side of mass installation of devices.
