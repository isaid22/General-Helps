To create a unique profile with different color side bars, I need to have a user settings.json file populated with these example values:

{
 "workbench.colorCustomizations": {
   "titleBar.activeBackground": "#8870ac",
   "statusBar.background": "#846ea7",
   "activityBar.background": "#5d457e",
   "sideBar.background": "#8f70b4",
   "focusBorder": "#9C27B0",
   "window.activeBorder": "#BA68C8",
   "window.inactiveBorder": "#c6addf",
   "window.titleBarStyle": "custom", "window.title": "${workspaceFolderBasename} | ${remoteName} | ${remoteAuthority}"
 }
}



To do so, I need to launch a new VS Code instance, then Ctrl + Shift + P (must be in this sequence)

Then type: Preferences: Open Settings (JSON)

It’s very possible you will see this instead: 

Preferences: Open User Settings (JSON)

Then replace whatever you see with the code snippet above.

Then save this file. The current profile will refresh this VS Code instance.


You may create a new profile name. 

New Window with Profile… -> New Profile -> Then give this profile a name, then select setting on the bottom, then click create, then double click on the setting with the word of new name, it should pop up a settings.json, which is empty. Now you fill in the code snippet above. Save it, and this new profile will persist in future use.

