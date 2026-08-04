# Eudora Unicode Fix

Eudora Unicode Fix is a 32-bit EMSAPI plug-in for Eudora 7.1.0.9 (and possibly earlier versions). It repairs
Gmail and other HTML messages containing UTF-8 mojibake, mathematical Unicode
letters, and Unicode byte sequences interrupted by HTML entities.

The primary deliverable is `EudoraUnicodeFix.dll`. 

> **Restart required:** Eudora must be completely closed and restarted after
> installing, replacing, updating, or removing a plug-in DLL. Eudora loads
> plug-ins only at startup and does not detect plug-in changes while running.

## Install

1. Close Eudora completely.
2. Back up your Eudora data and `Plugins` directories.
3. Copy `build\Release\EudoraUnicodeFix.dll` into Eudora's active `Plugins`
   directory.
4. Start Eudora.

To repair a message, double-click it so it opens in its own window, then choose
**Edit > Message Plug-ins > Repair Gmail Unicode for Eudora**. The command is
not available in the preview pane. Eudora will ask whether to save the modified
message when its window closes.

The plug-in runs only when requested; it does not alter incoming mail
automatically.

## Settings

Choose **Special > Message Plug-ins Settings**, select **EudoraUnicodeFix Rev
A**, and click **Settings**.

- **Repair mathematical Unicode styling** converts compatibility characters
  such as `𝐇𝐨𝐩𝐞` to ordinary text.
- **Repair UTF-8 mojibake** repairs text such as `â€™`, `Ã©`, and damaged
  four-byte Unicode sequences.
- **Conservative mode** requires repairs to pass validity and readability
  checks. Keeping it enabled is recommended.
- **Write diagnostic log** writes `%TEMP%\EudoraUnicodeFix.log`.
- **Save last input and output HTML** writes diagnostic snapshots in `%TEMP%`.
  These files can contain private message content and are disabled by default.
- **Show completion summary** displays how many HTML text sections were
  repaired after each run.
- **Open Log Folder** opens the Windows temporary directory.

Both repair modes, conservative mode, and logging are enabled by default.
Snapshots and completion summaries are disabled. Preferences are stored in
`EudoraUnicodeFix.ini` in Eudora's configuration directory, which is only read at Eudora startup.

## Troubleshooting

If the menus do not appear:

1. Confirm the DLL is in the active Eudora `Plugins` directory.
2. Confirm Eudora was completely closed before the DLL was replaced, then
   restart it.
3. Confirm the DLL is the Win32/x86 Release build.
4. Enable Eudora plug-in logging and look for `EudoraUnicodeFix.dll` followed by
   calls to `ems_plugin_version`, `ems_plugin_init`, and `ems_translator_info`.

The diagnostic log is created only when the repair command runs and logging is
enabled. Its absence does not by itself mean that plug-in startup failed.

## Safety and scope

- The translator accepts `text/html` messages only.
- It preserves HTML tags and attributes while repairing text nodes.
- It emits Windows-1252 text plus numeric HTML entities where needed.
- Conservative mode is intended to avoid speculative changes.
- Back up important mail before processing messages in bulk.

