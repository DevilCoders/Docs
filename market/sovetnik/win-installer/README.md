# win-installer

To compile without signing, just comment the SignTool key in commonsetup.iss and then compile.
To compile with signing (e.g. setup.iss), do `iscc /Ssigntool=signtool.exe setup.iss`.
The program is installed in program files for ease of updating, which happens under SYSTEM account.

To test silent install with affiliate IDs, use a command like this `extension-setup.exe /SP- /VERYSILENT /NOICONS /NOCANCEL /NORESTART /SUPPRESSMSGBOXES /affid=4321 /clid=4321 /vid=4321 /all=1`.
To test exit codes, use the "start /wait cmd /c yourapp.exe" command, then do "echo %errorLevel%".

Before compiling setup.iss, you must compile following tools:
    1. Helper C++ project in Release-Win32 configuration. (Don't forget to sign the PE file if there's a need.)
    2. Updater C++ project in Release-Win32 configuration. (Don't forget to sign this file, if needed.)
       Do know that while Helper exe gets its parameters from command line, Updater EXE has ALL its params hardcoded.
       So you have to set them to proper ones before compiling the EXE file (see top of Updater.cpp).
       For example, 'APP_ID' must be same as 'AppId' in 'common.iss' file.
       Don't compile in Win64 configuration so you can be sure it works on Win32 OS as well.
       'updatechecker.iss' is an alternative implementation of update check program using InnoSetup scripting, but it can't mark temp files for deletion on reboot.
    3. Put corresponding signed-for-distribution XPI in this root folder, and check that it equals the name specified in 'common.iss'. 
Then you can compile the 'setup.iss' and 'updater.iss' which will give you installer and updater packages.
Updater package should be placed on a CDN near 'version.txt' file (that will control updates on client machines).
Installer package can be used as-is (and launched silently using command line example from above).
