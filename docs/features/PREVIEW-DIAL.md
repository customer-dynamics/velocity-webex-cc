# Preview Dial

## Setup

### Add Widget to Desktop Layout

The Velocity Preview Dial widget is a full page widget that agents use in the Webex CC Desktop interface. This widget will need to be added to the desktop layout that your agents use. To find the desktop layouts currently in use, or to create a new one, navigate to the [_Desktop Layouts_ section in the Webex Contact Center settings](https://admin.webex.com/wxcc/desktop-experience/desktop-layouts) in Control Hub.

To add the widget, add the following to your desktop layout JSON file, in the `agent > area > navigation` section:

```json
{
  "nav": {
    "label": "Preview Dial",
    "icon": "https://velocity.customerdynamics.com/logo.svg",
    "iconType": "other",
    "navigateTo": "velocity-preview",
    "align": "top"
  },
  "page": {
    "id": "velocity-preview",
    "widgets": {
      "cdyx-vel-preview": {
        "comp": "cdyx-vel-preview",
        "script": "https://velocity.customerdynamics.com/assets/preview.js",
        "attributes": {
          "dark": "$STORE.app.darkMode"
        },
        "properties": {
          "accessToken": "$STORE.auth.accessToken",
          "outdialEp": "$STORE.agent.outDialEp",
          "velocityApiKey": "",
          "velocityAuth": "",
          "agentId": "$STORE.agent.agentId",
          "teamId": "$STORE.agent.teamId"
        }
      }
    },
    "layout": {
      "areas": [
        [
          "cdyx-vel-preview"
        ]
      ],
      "size": {
        "cols": [
          1
        ],
        "rows": [
          1
        ]
      }
    }
  }
},
```

### Define Widget Properties

Provide the appropriate values in the JSON above, using the following descriptions to guide you.

#### Script

The `script` to use for the widget depends on the environment used. For this value, use the URL that corresponds to your environment:

| Environment | Script URL                                            |
| ----------- | ----------------------------------------------------- |
| Development | `https://velocity-dev.cd-ccs.net/assets/preview.js`       |
| Staging     | `https://velocity-staging.cd-ccs.net/assets/preview.js`   |
| Production  | `https://velocity.customerdynamics.com/assets/preview.js` |

> [!NOTE]
> Unless otherwise specified for your tenant, use the production script.

#### General Configuration

| Value            | Description                                                                                                                                                                                                                                                                                                                  |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `velocityApiKey` | The API key for your Velocity tenant.                                                                                                                                                                                                                                                                                        |
| `velocityAuth`   | The credentials of a Velocity account. This will be a system account used for all agents in your organization; it does not have to be the credentials for the agent using preview dial. To get this value, [Base64-encode](https://www.base64encode.org/) your credentials in the format `username:password` (note the colon). |

### Add Headless Widget

In order for calls to be correctly dispositioned, you will also need to add a headless widget to the desktop layout. This widget will not be visible to agents, but is required for the preview dial widget to function properly.

Add the following to your desktop layout JSON file, in the `agent > area > headless` section:

```json
"headless": {
  "id": "velocity-headless",
  "widgets": {
    "cdyx-vel-headless": {
      "comp": "cdyx-vel-headless",
      "script": "https://velocity.customerdynamics.com/assets/headless.js",
      "attributes": {
        "dark": "$STORE.app.darkMode"
      },
      "properties": {
        "teamId": "$STORE.agent.teamId",
        "velocityApiKey": "",
        "velocityAuth": "",
        "agentId": "$STORE.agent.agentId"
      }
    }
  },
  "layout": {
    "areas": [
      [
        "cdyx-vel-headless"
      ]
    ],
    "size": {
      "cols": [
        1
      ],
      "rows": [
        1
      ]
    }
  }
}
```

### Define Headless Widget Properties

Provide the appropriate values in the JSON above, using the following descriptions to guide you.

#### Headless Script

The `script` to use for the widget depends on the environment used. For this value, use the URL that corresponds to your environment:

| Environment | Script URL                                                 |
| ----------- | ---------------------------------------------------------- |
| Development | `https://velocity-dev.cd-ccs.net/assets/headless.js`       |
| Staging     | `https://velocity-staging.cd-ccs.net/assets/headless.js`   |
| Production  | `https://velocity.customerdynamics.com/assets/headless.js` |

> [!NOTE]
> Unless otherwise specified for your tenant, use the production script.

#### General Headless Configuration

Use the same values for `velocityApiKey`, and `velocityAuth` as you did for the preview dial widget.
