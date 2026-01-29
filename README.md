# Taskbar Toggler. Releases
This repo will contain any public releases of Taskbar Toggler. This Windows 10/11 app allows to switch between Shown and Hidden Taskbar. It adds an option to the Expanded Context Menu (right-click + Show more options) that switches the Taskbar Behavior.

YouTube showcase: https://youtu.be/b4HsW2EmmvI

# Tired of going through settings to hide the task bar? Me too
* It is a lightweight, seamless, fully local application. None of your information/setting is stored online.
* The app runs only when clicked, executes the toggle, and immediately closes. It does not run in the background.
* Works on all your monitors 
* Does not require Startup

## Two modes are supported:
1. Desktop-only. Appears only in the Desktop background Context Menu. [This is set by default]
2. All folders. Appears in the Context Menu in any folder Context Menu
* If you want to change this, simply open the application, select Re-Install, then choose which behavior you would like to use. The application will clean up previous installation and reinstall itself how you wanted it.

## How It Works

### 1. The Win32 API
The application uses Platform Invocation Services (P/Invoke) to interact directly with the Windows Shell.
* **`FindWindow("Shell_TrayWnd", null)`**: Locates the handle (HWND) of the primary taskbar.
* **`SHAppBarMessage`**: The core function from `shell32.dll` used to get and set the appbar state.
* **State Logic**: It queries the current state (checked via `ABM_GETSTATE`). If the `ABS_AUTOHIDE` bit is set, it removes it. If it is missing, it adds it. Finally, it broadcasts the new state via `ABM_SETSTATE`.

### 2. Registry Integration
To appear in the right-click menu, the installer writes to:
* Desktop only:
`HKEY_CURRENT_USER\Software\Classes\DesktopBackground\shell\TaskbarToggler`
* Any folder:
`HKEY_CURRENT_USER\Software\Classes\Directory\Background\shell\TaskbarToggler`

### Installation file
* Created using Inno Setup Compiler and .NET 10
* Uninstall file included. Also can be uninstalled through Start Menu (Windows Application List)

### Antivirus
*  I am working on publishing this on Microsoft Store. 
*  Since I am an independent developer, you may encounter a Smart Screen warning when downloading the executable installation wizard from GitHub. You can ignore the message by clicking 'More Info' -> 'Run Anyway' to proceed.
* I am not asking you to turn off your Antivirus software

## Bugs
* Please report any Issues to the Issues tab
