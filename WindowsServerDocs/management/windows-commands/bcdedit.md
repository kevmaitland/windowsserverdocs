---
title: bcdedit
description: "Windows Commands topic for **bcdedit** - create new stores, modify existing stores, and add boot menu parameters."
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab2da47d-3aac-44a0-b7fd-bd9561d61553
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# bcdedit

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Boot Configuration Data (Bcd) files provide a store that is used to describe boot applications and boot application settings. The objects and elements in the store effectively replace Boot.ini.
bcdedit is a command-line tool for managing Bcd stores. It can be used for a variety of purposes, including creating new stores, modifying existing stores, adding boot menu parameters, and so on. bcdedit serves essentially the same purpose as bootcfg.exe on earlier versions of Windows, but with two major improvements:
-   exposes a wider range of boot parameters than bootcfg.exe.
-   Has improved scripting support.
> [!NOTE]
> Administrative privileges are required to use bcdedit to modify Bcd.
bcdedit is the primary tool for editing the boot configuration of Windows Vista and later versions of Windows. It is included with the Windows Vista distribution in the %WINdir%\System32 folder.
bcdedit is limited to the standard data types and is designed primarily to perform single common changes to Bcd. for more complex operations or nonstandard data types, consider using the Bcd Windows Management Instrumentation (WMI) application programming interface (API) to create more powerful and flexible custom tools.
## Syntax
```
bcdedit /Command [<Argument1>] [<Argument2>] ...
```
## Parameters
### General bcdedit Command-Line Option
|Option|Description|
|-----|--------|
|/?|Displays a list of bcdedit commands. Running this command without an argument displays a summary of the available commands. To display detailed help for a particular command, run **bcdedit /?** <command>, where <command> is the name of the command you are searching for more information about. for example, **bcdedit /? createstore** displays detailed help for the createstore command.|
### Parameters that Operate on a Store
|Option|Description|
|-----|--------|
|/createstore|creates a new empty boot configuration data store. The created store is not a system store.|
|/export|Exports the contents of the system store into a file. This file can be used later to restore the state of the system store. This command is valid only for the system store.|
|/import|Restores the state of the system store by using a backup data file previously generated by using the **/export** option. This command deletes any existing entries in the system store before the import takes place. This command is valid only for the system store.|
|/store|This option can be used with most bcdedit commands to specify the store to be used. if this option is not specified, then bcdedit operates on the system store. Running the **bcdedit /store** command by itself is equivalent to running the **bcdedit /enum active** command.|
### Parameters that Operate on Entries in a Store
|Parameter|Description|
|-------|--------|
|/copy|Makes a copy of a specified boot entry in the same system store.|
|/create|creates a new entry in the boot configuration data store. if a well-known identifier is specified, then the **/application**, **/inherit**, and **/device** parameters cannot be specified. if an identifier is not specified or not well known, an **/application**, **/inherit**, or **/device** option must be specified.|
|/delete|deletes an element from a specified entry.|
### Parameters that Operate on Entry Options
|Parameter|Description|
|-------|--------|
|/deletevalue|deletes a specified element from a boot entry.|
|/set|Sets an entry option value.|
### Parameters that Control Output
|Parameter|Description|
|-------|--------|
|/enum|lists entries in a store. The **/enum** option is the default value for BCedit, so running the **bcdedit** command without parameters is equivalent to running the **bcdedit /enum active** command.|
|/v|verbose mode. Usually, any well-known entry identifiers are represented by their friendly shorthand form. Specifying **/v** as a command-line option displays all identifiers in full. Running the **bcdedit /v** command by itself is equivalent to running the **bcdedit /enum active /v** command.|
### Parameters that Control the Boot Manager
|Parameter|Description|
|-------|--------|
|/bootsequence|Specifies a one-time display order to be used for the next boot. This command is similar to the **/displayorder** option, except that it is used only the next time the computer starts. Afterwards, the computer reverts to the original display order.|
|/default|Specifies the default entry that the boot manager selects when the timeout expires.|
|/displayorder|Specifies the display order that the boot manager uses when displaying boot parameters to a user.|
|/timeout|Specifies the time to wait, in seconds, before the boot manager selects the default entry.|
|/toolsdisplayorder|Specifies the display order for the boot manager to use when displaying the **Tools** menu.|
### Parameters that Control Emergency Management Services
|Parameter|Description|
|-------|--------|
|/bootems|Enables or disables Emergency Management Services (EMS) for the specified entry.|
|/ems|Enables or disables EMS for the specified operating system boot entry.|
|/emssettings|Sets the global EMS settings for the computer. **/emssettings** does not enable or disable EMS for any particular boot entry.|
### Parameters that Control Debugging
|Parameter|Description|
|-------|--------|
|/bootdebug|Enables or disables the boot debugger for a specified boot entry. Although this command works for any boot entry, it is effective only for boot applications.|
|/dbgsettings|Specifies or displays the global debugger settings for the system. This command does not enable or disable the kernel debugger; use the **/debug** option for that purpose. To set an individual global debugger setting, use the **bcdedit /set** <dbgsettings> <type> <value> command.|
|/debug|Enables or disables the kernel debugger for a specified boot entry.|
## Examples
for examples of bcdedit, see the [Windows Hardware Developer Center Web site](http://go.microsoft.com/fwlink/?LinkId=69448).