# netlify-dev-vs-code-launch-config
Launch Configuration to run the netlify cli with netlify dev attached to the Chrome browser and vs code node debugger instances

## launch.json

```JSON
{
  "version": "0.2.0",
  "compounds": [
    {
      "name": "Netlify Dev Chrome",
      "configurations": ["Launch Chrome", "netlify dev"],
      "stopAll": true
    }
  ],
  "configurations": [
    {
      "name": "Launch Chrome",
      "request": "launch",
      "type": "pwa-chrome",
      "url": "http://localhost:8888",
      "webRoot": "${workspaceFolder}"
    },
    {
      "name": "netlify dev",
      "type": "node",
      "request": "launch",
      "skipFiles": ["<node_internals>/**"],
      "outFiles": ["${workspaceFolder}/.netlify/functions-serve/**/*.js"],
      "program": "${workspaceFolder}/node_modules/netlify-cli/bin/run",
      "args": ["dev"],
      "console": "integratedTerminal",
      "env": { "BROWSER": "none" },
      "serverReadyAction": {
        "pattern": "Server now ready on (https?://[w:.-]+)",
        "uriFormat": "%s",
        "action": "debugWithChrome"
      }
    },
    {
      "name": "netlify functions:serve",
      "type": "node",
      "request": "launch",
      "skipFiles": ["<node_internals>/**"],
      "outFiles": ["${workspaceFolder}/.netlify/functions-serve/**/*.js"],
      "program": "${workspaceFolder}/node_modules/.bin/netlify",
      "args": ["functions:serve"],
      "console": "integratedTerminal"
    }
  ]
}
```


## See Reference
- https://github.com/netlify/cli/blob/main/docs/vscode.md
