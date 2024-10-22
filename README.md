# OSD-InstallCompanyPortal
Scripts to use in an OSD Task Sequence to get Company Portal installed. 

CompanyPortalScheduledTask.ps1

Purpose
This script is designed to create and register a scheduled task that runs a PowerShell script (InstallCompanyPortal.ps1) located in a directory specified by the PackageID parameter.

Parameters
$PackageID: A string parameter that represents the ID of the package. This ID is used to construct the path to the InstallCompanyPortal.ps1 script.
Script Path
$scriptPath: Constructs the full path to the InstallCompanyPortal.ps1 script using the provided PackageID.
Task Action
$action: Defines the action for the scheduled task. It specifies that powershell.exe should be executed with the argument to run the script located at $scriptPath.
Task Trigger
$trigger: Sets the trigger for the scheduled task to run at logon.
Task Principal
$principal: Defines the principal (user context) under which the task will run. It specifies that the task should run for users in the "Users" group, with an interactive logon type and the highest run level (admin privileges).
Task Settings
$settings: Configures additional settings for the scheduled task. It allows the task to start if the computer is on battery power, ensures the task doesn't stop if the computer switches to battery power, and starts the task as soon as possible if a scheduled start is missed.
Create and Register Task
$task: Creates a new scheduled task with the specified action, principal, trigger, and settings.
Register-ScheduledTask: Registers the newly created task with the name "InstallCompanyPortal".
Summary
This script automates the creation and registration of a scheduled task that runs a specific PowerShell script at user logon, with elevated privileges and specific settings to handle battery power scenarios.



CompanyPortalInstaller.ps1

This PowerShell script is designed to install the Company Portal application using WinGet, a package manager for Windows. Here's a step-by-step explanation of what the script does:

Set Progress Preference:

This line sets the $progressPreference variable to 'silentlyContinue', which suppresses the progress bar output during the script execution.

Check for WinGet Installation:

This line checks if WinGet is already installed by trying to get the package named Microsoft.Winget.Source.

Conditional Installation of WinGet:

If WinGet is not installed ($winGet is null or empty), the script:

Writes an informational message.
(Commented out) Downloads the necessary files for WinGet and its dependencies using Invoke-WebRequest.
Installs the downloaded files using Add-AppxPackage.
Install Company Portal:

This line installs the Company Portal application using WinGet with the specified options to run silently, force the installation, and accept package and source agreements.

Wait for Installation to Complete:

The script pauses for 120 seconds to allow the installation to complete.

Remove Scheduled Task if Company Portal is Installed:

The script checks if the Company Portal application is installed. If it is, it removes a scheduled task named "InstallCompanyPortal" without asking for confirmation.

Key Points:
Suppress Progress Bar: $progressPreference = 'silentlyContinue'
Check for Existing Installation: Get-AppxPackage -Name Microsoft.Winget.Source
Conditional Installation: Downloads and installs dependencies if WinGet is not present.
Install Company Portal: Uses WinGet to install the application.
Wait for Completion: Start-Sleep -Seconds 120
Clean Up: Removes a scheduled task if the Company Portal is installed.
This script is useful for automating the installation of the Company Portal application, ensuring that all necessary dependencies are in place, and cleaning up after the installation.
