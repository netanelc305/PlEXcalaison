# Local Privilege PlEXcalasion 

## Discovered by
Tomer Peled, Netanel Cohen, and Amir Shen a Security Researchers from BugSec.

## Description
Plex Media Server for windows vulnerable to Time Of Check Time Of Use (TOCTOU) which allows low privilege users to gain SYSTEM privileges. 

## Details
Plex for windows used PlexUpdateService.exe to install new updates. the service is running in the SYSTEM context. When installing the update, the service will first verify the update file was not modified and was signed by plex only then the new update will be installed.

However, A design flow exists in this process. After the integrity and signature check, the file is closed and reopened later for installation.

This flaw allows an attacker to swap the update file as soon as the service is finished to verify the integrity and signature, resulting in code execution in the SYSTEM context.

 

This POC use tools developed by James Forshaw with slight modifications. The original can be found here - https://github.com/googleprojectzero/symboliclink-testing-tools

In addition we have created an RPC client that will trigger the update.




## Usage

1. Clone the repository and open PlEXcalasion.sln in Visual Studio.
2. Modify Paths:

PlexClient/PlexClient.cpp replace ROOTDIR with your path.
```cpp
const wchar_t* pszString = L"<ROOTDIR>\\PlEXcalaison\\TOCTOU\\junction\\plex.exe"; // Path to the update file. 
```
PlEXcalaison/BaitAndSwitch/BaitAndSwitch.cpp replace ROOTDIR with your path.
```cpp
static LPCWSTR junction = L"<ROOTDIR>\\PlEXcalaison\\TOCTOU\\junction";  // Path to junction folder , MAKE SURE IT IS EMPTY !
static LPCWSTR target1 = L"<ROOTDIR>\\PlEXcalaison\\TOCTOU\\valid"; // Path to folder contains the valid update file.
static LPCWSTR target2 = L"<ROOTDIR>\\PlEXcalaison\\TOCTOU\\malicious"; // Path to folder contains the malicious file - MUST BE THE SAME NAME AS THE UPDATE FILE.
static LPCWSTR cacert = L"C:\\Program Files (x86)\\Plex\\Plex Media Server\\Resources\\cacert.pem"; // Path to cacert.pem - can be found in plex directory.
```

3. Build the solution.
4. Make sure a PlexClient.exe was created and can be found on Rleases dir.
5. Put the desired executeable file you want to execute as system in the malicious folder and rename it to plex.exe (for the poc i used cmd.exe)
6. Execute BiteAndSwap.exe



