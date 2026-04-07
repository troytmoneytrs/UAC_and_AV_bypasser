# UAC_and_AV_bypasser
# UAC and AV Bypasser

This tool is a C# console application designed to bypass User Account Control (UAC) on Windows systems and provides functionalities to interact with and manage various antivirus (AV) solutions. It features an interactive shell interface, "Vortex Shell," for easy command execution.

## Features

*   **UAC Bypass**: Elevates privileges by hijacking the `ms-settings` protocol handler via the registry and triggering it with `computerdefaults.exe`.
*   **Interactive Shell**: A custom "Vortex Shell" for executing commands.
*   **Antivirus Detection**: Scans and lists installed antivirus products using WMI (`SecurityCenter2`), displaying their status.
*   **Antivirus Management Modules**: Provides dedicated sub-shells to configure and disable components of popular AV solutions:
    *   Windows Defender
    *   McAfee / Trellix
    *   Avast
    *   AVG
    *   Avira
    *   Norton

## How It Works

The UAC bypass technique involves the following steps:
1.  A new registry key is created under `HKEY_CURRENT_USER\Software\Classes\ms-settings\Shell\Open\command`.
2.  The default value of this key is set to the path of the executable you want to run with elevated permissions.
3.  A `DelegateExecute` string value is created to enable the handler.
4.  The `computerdefaults.exe` process is started, which triggers this registry key, executing the target application with high privileges.
5.  The tool automatically cleans up the created registry keys after execution.

## Usage

Run the executable to launch the `UAC-Bypasser` interactive shell.

```
UAC-Bypasser>
```

Type `help` to see a list of available commands.

### Main Commands

| Command                 | Description                                                              |
| ----------------------- | ------------------------------------------------------------------------ |
| `run <path>`            | Executes a binary with elevated (SYSTEM) privileges using the UAC bypass. |
| `av`, `av -l`           | Lists all detected antivirus products and their status.                  |
| `wd`                    | Enters the Windows Defender management sub-shell.                        |
| `mcafee`, `mfe`         | Enters the McAfee/Trellix management sub-shell.                          |
| `avast`                 | Enters the Avast management sub-shell.                                   |
| `avg`                   | Enters the AVG management sub-shell.                                     |
| `avira`                 | Enters the Avira management sub-shell.                                   |
| `norton`                | Enters the Norton management sub-shell.                                  |
| `help`                  | Displays the help message with all commands.                             |
| `clear`                 | Clears the terminal screen.                                              |
| `exit`, `quit`          | Exits the application.                                                   |

**Example:** To open an elevated Command Prompt:
```
UAC-Bypasser> run "C:\Windows\System32\cmd.exe"
```

### Windows Defender Sub-shell

The `wd` command opens a dedicated shell for managing Windows Defender features.

**Sub-commands:**
*   `disable -<feature>`: Disables a specific feature.
*   `enable -<feature>`: Enables a specific feature.

**Features:**
*   `-realtime`: Real-Time Monitoring
*   `-behavior`: Behavior Monitoring
*   `-ips`: Network Intrusion Prevention System
*   `-script`: Script Scanning
*   `-all`: Applies the action to all available features.

**Example:** To disable real-time protection:
```
UAC-Bypasser/windows-defender> disable -realtime
```

## Disclaimer

This tool is intended for educational and research purposes only. The author is not responsible for any misuse or damage caused by this program. Use it only on systems you have explicit permission to test.
