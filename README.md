How to Download Content Data Files and Patches Using the Download PowerShell Script
Products / Topics :
Security Controls, Patch for SCCM, Patch for Windows
Created Date
Dec 15, 2018 10:13:47 AM
Last Modified Date
Jan 4, 2024 6:02:06 PM
How To
Using the PowerShell script provided in this document, content data and patches are able to be downloaded from an internet connected machine and then transferred to an offline/disconnected console for scanning and patching.

This can also be used as a workaround if connections cannot be made to Ivanti or Vendor resources for patch and file downloads.
How To - Answer
Prerequisites to use this PowerShell script:

    Windows PowerShell 4.0 or later
    Microsoft .NET Framework 4.7.2.461808 or later
    Windows Management Framework 5.1
    The PowerShell script .\DownloadDisconnectedData.ps1 (attached to this document)
    The machine running the script must be connected to the Internet in order to successfully download the intended files

Console Datafiles Locations

    C:\ProgramData\Ivanti\Security Controls\Console\DataFiles

How to download content data files: (no patches)
1. Create a folder on the internet connected machine on C:\. (this example will use C:\Data)
2. Download and extract the PowerShell script (DownloadDisconnectedData.zip) attached to this document to C:\Data.
NOTE: Right-click the zip and check Properties to make sure the file is not blocked before extracting. If necessary, check the box to Unblock and click Apply or OK.
User-added image
3. Open PowerShell and navigate to C:\Data.
4. Run the following command replacing C:\Data with whatever output directory you have chosen in step 1:

NOTE: Use the value corresponding to your version:

    Security Controls 2023.4 and up:

.\DownloadDisconnectedData.ps1 -outdir "C:\Data" -product "Isec" -version 9.6

    Security Controls 2021.4 - 2023.3:

.\DownloadDisconnectedData.ps1 -outdir "C:\Data" -product "Isec" -version 9.5

    OEM SDK 9.3:

.\DownloadDisconnectedData.ps1 -outdir "C:\Data" -product "OEM" -version 93 -company "genericCompany"

5. Move the downloaded data files from C:\Data to the DataFiles folder on the offline Security Controls console (see paths here). Overwrite any duplicate files when prompted.
6. Click Help > "Refresh files" in the console. If you are in an offline environment, you will see errors downloading files which is to be expected, but after the failed downloads it will then update the database with the newest definitions.

How to download patches: (no content)

How to create the list of patches to download:

    Create a folder on the internet connected machine on C:\. (this example will use C:\Data)
    Scan machines on your disconnected network. (The scan result will provide the list of patches to be downloaded)
    View the scan results after the scan completes by clicking 'View results' in the Operations monitor.
    Highlight and then right-click on any missing patches in the middle pane and choose Export Download Package…
        You can also choose specific patches using the CTRL-click or Shift-click method after expanding the missing patches list.

User-added image

     5. Give the .CSV a name and save to your desktop. (we will be using Patches.csv in this example)

image.png   

     6. Save this .CSV file to the folder you create in step #1.

To use the PowerShell script:

    Move the DownloadDisconnectedData.zip to the folder you created on the internet connected machine on C:\.
    Extract the PowerShell script (DownloadDisconnectedData.ps1).
    Open a PowerShell prompt with elevated privileges (Run as administrator).
    Change to the directory that contains the PowerShell script.
    Read Disclaimer.txt.
    Use the PowerShell script to download the desired files. Please see the PowerShell script information section below for information on how to do this.
        Security Controls 2023.4 and up:

.\DownloadDisconnectedData.ps1 -outdir "C:\Data" -product "Isec" -version 9.6 -downloadPackageInputFilePath "C:\Data\Patches.csv" -doNOTDwnlDataFile

    Security Controls 2021.4 - 2023.3:

.\DownloadDisconnectedData.ps1 -outdir "C:\Data" -product "Isec" -version 9.5 -downloadPackageInputFilePath "C:\Data\Patches.csv" -doNOTDwnlDataFile

    OEM SDK 9.3:

.\DownloadDisconnectedData.ps1 -outdir "C:\Data" -product "OEM" -version 93 -downloadPackageInputFilePath "C:\Data\Patches.csv" -doNOTDwnlDataFile

    Move the downloaded datafiles from the downloaded location specified to Datafiles folder on the offline Security Controls console (see paths here). Overwrite any duplicate files when prompted.
    Move the downloaded patches from the downloaded location to your console's patch repository which can be located in Tools > Options > Downloads.
    Click Help > "Refresh files" in the console. If you are in an offline environment, you will see errors downloading files which is to be expected, but after the failed downloads it will then update the database with the newest definitions.

 

NOTE: If you receive an error stating “execution of scripts is disabled on this system” you can enable execution by running the following command:

set-executionpolicy RemoteSigned

 
Related Files
DownloadDisconnectedData_04202022
Applies to

Patch for SCCM - Patch for MEM 2022.4, Patch for SCCM 2.4, Patch for SCCM 2019.2

Patch for Windows - Patch for Windows 9.3
Article Number :
000002112
Article Promotion Level
Normal

https://forums.ivanti.com/s/article/How-To-Download-Content-Data-Files-and-Patches-using-the-Download-PowerShell-Script?language=en_US
 

