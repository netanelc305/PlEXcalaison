symboliclink-testing-tools

(c) Google Inc. 2015
Developed by James Forshaw

This is a small suite of tools to test various symbolic link types of Windows. It consists of the following
tools:

BaitAndSwitch : Creates a symbolic link and uses an OPLOCK to win a TOCTOU
CreateDosDeviceSymlink: Creates a object manager symbolic link using csrss
CreateMountPoint: Create an arbitrary file mount point
CreateNtfsSymlink: Create an NTFS symbolic link
CreateObjectDirectory: Create a new object manager directory
CreateRegSymlink: Create a registry key symbolic link
DeleteMountPoint: Delete a mount point
DumpReparsePoint: Delete the reparse point data
NativeSymlink: Create an object manager symbolic link
SetOpLock: Tool to create oplocks on arbitrary files or directories

The tools can be built with Visual Studio 2013