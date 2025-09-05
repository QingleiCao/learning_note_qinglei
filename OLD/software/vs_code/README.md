# Download

https://code.visualstudio.com/

# Remote ssh (tested on Mac)

https://code.visualstudio.com/docs/remote/ssh

# Settings

## Terminal word jump

Add the following codes in `keybindings.json` (F1 or ⇧⌘p, then search `Open Keyboard Shortcuts (JSON)`):
```
        {
                "key": "ctrl+b",
                "command": "workbench.action.terminal.sendSequence",
                "args": { "text": "\u001bb" },
                "when":"terminalFocus"
        },
        {
                "key": "ctrl+f",
                "command": "workbench.action.terminal.sendSequence",
                "args": { "text": "\u001bf" },
                "when":"terminalFocus"
        }
```

## Fontsize

In `Open User Settings (JSON)`, replace it with the following codes, where `window.zoomLevel` controls the fontsize of sidebar:
```
{
    "cmake.configureOnOpen": true,
    "editor.fontSize": 16,
    "[python]": {
        "editor.formatOnType": true
    },
    "editor.tabSize": 8,
    "terminal.integrated.fontSize": 16,
    "editor.accessibilityPageSize": 16,
    "window.zoomLevel": 0.8,
    "editor.scrollbar.horizontalScrollbarSize": 16,
    "git.ignoreLegacyWarning": true,
    "terminal.integrated.enableMultiLinePasteWarning": false
}
```

## Extensions

ctags, git, c, c++, etc.

