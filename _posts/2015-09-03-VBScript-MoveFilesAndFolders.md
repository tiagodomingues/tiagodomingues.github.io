---
layout: post
title: VB Script - Move Files And Folders
---

>:: Back up select files and folders to a location
@echo off

>:: Set Variables
set destinationDrive=d:
set destinationPath=backup
Set destination=%destinationDrive%\%destinationPath%
set validationFile="C:\Pasta\novo.txt"

>echo INICIO às %date% %time% > c:\%date%.txt

>:: Check to see if the drive is available
if not exist %destinationDrive%\. goto :nodestinationDrive 
:: Move to destination drive
%destinationDrive%
echo %date% %time%: Network Drive OK >> c:\%date%.txt

>:: Check to see if the path is available
if not exist "\%destinationPath%\." goto :nodestinationPath
:: Move to destination path
cd %destinationPath%
echo %date% %time%: Network Path OK >> c:\%date%.txt

>:: Check to see if the validation file exists
if not exist %validationFile% goto :novalidationFile
echo %date% %time%: File OK >> c:\%date%.txt

>:: Backup location is valid
@echo The backup location "%destination%" is valid. >> c:\%date%.txt

>:: Copy files and folders if source is newer than destination

>:: Desktop
@xcopy "C:\Pasta\novo.txt" "%destination%" /d /e /c /i /q /h /r /k /y
echo %date% %time%: Copied OK >> c:\%date%.txt
if exist "D:\Backup\novo.txt" move /y "C:\Pasta\novo.txt" D:\Teste\ 
echo %date% %time%: Moved OK >> c:\%date%.txt

>@echo.
@echo Files copied.  Please review output for errors.
@exit
goto eof

>:nodestinationDrive
@echo The destination drive "%destinationDrive%" does not exist. >> c:\%date%.txt
goto :nocopy

>:nodestinationPath
@echo The destination path "%destinationPath%" does not exist on drive %destinationDrive%. >> c:\%date%.txt
goto :nocopy

>:novalidationFile
@echo The validation file does not exist. >> c:\%date%.txt
goto :nocopy

>:: No files have been copied
:nocopy
::@echo A valid backup location cannot be confirmed.
echo %date% %time%: No files have been copied >> c:\%date%.txt
@echo No files have been copied.

>echo FIM às %date% %time% >> c:\%date%.txt

>cls
@exit