# OBS Autostart Setup

Setup to autostart OBS on boot and start replay buffer automatically without the shutdown check popup to make it as seamless as possible like Shadowplay.

# Task 1: OBS Autostart
<details>
<summary> Click to expand/close </summary>

## General
- Open <code>Task Scheduler</code> > <code>Create task</code> > Name: <code>OBS Autostart</code>
- Enable <code>Run only when user is logged on</code> and <code>Run with highest privileges</code>

![General Tab](https://i.imgur.com/74c73sS.png)
## Triggers
- Go to <code>Triggers</code> > New > Begin the task: <code>At log on</code>
- Delay task for: <code>30 seconds</code> and <code>Enable</code>> at the bottom.
- Click OK.

![Triggers Tab](https://i.imgur.com/9P6ShqR.png)
## Actions
- Go to <code>Actions</code> > New > Action: <code>Start a program</code>
- Program/script: <code>"C:\Program Files\obs-studio\bin\64bit\obs64.exe"</code> (or your own obs64.exe path)
- Add arguments: <code>--startreplaybuffer</code> (start replay buffer automatically, optional) and
<code>--minimize-to-tray</code> (start OBS minimized to tray, optional if you don't have the OBS system tray setting enabled already).
- Start in: <code>C:\Program Files\obs-studio\bin\64bit</code> (or your own obs64.exe path without the executable)
- Click OK.

![Actions Tab](https://i.imgur.com/rayfe7v.png)
## Conditions
- Go to <code>Conditions</code> and make sure everything is unchecked.

![Conditions Tab](https://i.imgur.com/XKomq5w.png)
## Settings
- Go to <code>Settings</code> and make sure everything is unchecked except <code>Allow task to be run on demand</code>
and <code> If the running task does not end when requested, force it to stop</code>.
- Click OK.

![Settings Tab](https://i.imgur.com/dIbfdq1.png)
</details>

# Task 2: Disable OBS Shutdown Check
<details>
<summary> Click to expand/close </summary>

## General
- Open <code>Task Scheduler</code> > <code>Create task</code> > Name: <code>OBS Disable Shutdown Check</code>
- Enable <code>Run only when user is logged on</code>.

![General Tab](https://i.imgur.com/CcsC1Nn.png)
## Triggers
- Go to <code>Triggers</code> > New > Begin the task: <code> At log on</code>
- No delay, only select <code>Enable</code> at the bottom.
- Click OK.

![Triggers Tab](https://i.imgur.com/oaY4BrO.png)
## Actions
- Go to <code>Actions</code> > New > Action: <code>Start a program</code>
- Program/script: <code>cmd.exe</code>
- Add arguments: <code>/c "rd /s /q %APPDATA%\obs-studio\.sentinel"</code> (This is a workaround for the now removed --disable-shutdown-check command that OBS removed with version 32.0.0 that makes it so there's no popup saying you shutdown OBS wrongly on a fresh boot)

![Actions Tab](https://i.imgur.com/iasHONz.png)
## Conditions
- Go to <code>Conditions</code> and make sure everything is unchecked.

![Conditions Tab](https://i.imgur.com/4RHyJjF.png)
## Settings
- Go to <code>Settings</code> and same as the other task (pretty sure the "stop if running more than X days doesn't matter)
- Click OK.

![Settings Tab](https://i.imgur.com/zKFtx9m.png)
</details>
