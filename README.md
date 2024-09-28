Code:
@echo off
title User Assistant

:main_menu
cls
echo =======================================
echo Welcome to the assistant program!
echo =======================================
echo 1. Check IP address
echo 2. Schedule computer shutdown
echo 3. Create a backup of files
echo 4. Exit
echo =======================================
set /p choice="Choose an action (1-4): "

if %choice%==1 goto check_ip
if %choice%==2 goto shutdown_timer
if %choice%==3 goto backup_files
if %choice%==4 goto exit_program

:: If the input is incorrect, return to the main menu
echo Error: Enter a number from 1 to 4.
pause
goto main_menu

:check_ip
cls
echo ============================
echo Checking the computer's IP address
echo ============================
for /f "tokens=2 delims=:" %%i in ('ipconfig ^| find "IPv4"') do set ip=%%i
echo Your IP address: %ip%
echo ============================
pause
goto main_menu

:shutdown_timer
cls
echo ============================
echo Schedule computer shutdown
echo ============================
set /p time="Enter the number of minutes until shutdown: "
set /a seconds=%time%*60
shutdown -s -t %seconds%
echo ============================
echo The computer will shut down in %time% minutes.
echo Press any key to return to the menu.
pause
goto main_menu

:backup_files
cls
echo ============================
echo Creating a backup of files
echo ============================
set /p source="Enter the path to the source folder for backup: "
set /p destination="Enter the path to the destination folder: "

:: Check if the destination folder exists
if not exist "%destination%" mkdir "%destination%"

:: Copy files
xcopy "%source%\*" "%destination%\" /s /i /y

echo ============================
echo Backup completed.
echo Files from %source% have been copied to %destination%.
echo Press any key to return to the menu.
pause
goto main_menu

:exit_program
cls
echo ============================
echo Thank you for using the program!
echo ============================
pause
exit
