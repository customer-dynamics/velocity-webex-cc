# Callbacks

## Setup

For callbacks in Velocity, there are two widgets available for agents use in the Webex CC Desktop interface. _Callbacks_ is a full page widget to display a list of the available callbacks to be dialed and _Callback_ is a panel widget to schedule a callback while on a call.

**Both** widgets will need to be added to the desktop layout that your agents use. To find the desktop layouts currently in use, or to create a new one, navigate to the [_Desktop Layouts_ section in the Webex Contact Center settings](https://admin.webex.com/wxcc/desktop-experience/desktop-layouts) in Control Hub.

### Callbacks Widget

#### Add Widget to Desktop Layout

To add the widget, add the following to your desktop layout JSON file, in the `agent > area > navigation` section:

```json
{
  "nav": {
    "label": "Callbacks",
    "icon": "https://velocity.customerdynamics.com/logo.svg",
    "iconType": "other",
    "navigateTo": "velocity-callback",
    "align": "top"
  },
  "page": {
    "id": "velocity-callback",
    "widgets": {
      "cdyx-vel-callback": {
        "comp": "cdyx-vel-callback",
        "script": "https://velocity.customerdynamics.com/assets/callback.js",
        "attributes": {
          "dark": "$STORE.app.darkMode"
        },
        "properties": {
          "accessToken": "$STORE.auth.accessToken",
          "outdialEp": "$STORE.agent.outDialEp",
          "velocityApiKey": "",
          "velocityAuth": "",
          "agentId": "$STORE.agent.agentId",
          "teamId": "$STORE.agent.teamId",
          "agentName": "$STORE.agent.agentName",
          "callback": true
        }
      }
    },
    "layout": {
      "areas": [
        [
          "cdyx-vel-callback"
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

#### Define Widget Properties

Provide the appropriate values in the JSON above, using the following descriptions to guide you.

##### Script

The `script` to use for the widget depends on the environment used. For this value, use the URL that corresponds to your environment:

| Environment | Script URL                                                 |
| ----------- | ---------------------------------------------------------- |
| Development | `https://velocity-dev.cd-ccs.net/assets/callback.js`       |
| Staging     | `https://velocity-staging.cd-ccs.net/assets/callback.js`   |
| Production  | `https://velocity.customerdynamics.com/assets/callback.js` |

> [!NOTE]
> Unless otherwise specified for your tenant, use the production script.

##### General Configuration

| Value            | Description                                                                                                                                                                                                                                                                                                                  |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `velocityApiKey` | The API key for your Velocity tenant.                                                                                                                                                                                                                                                                                        |
| `velocityAuth`   | The credentials of a Velocity account. This will be a system account used for all agents in your organization; it does not have to be the credentials for the agent using Click2Call. To get this value, [Base64-encode](https://www.base64encode.org/) your credentials in the format `username:password` (note the colon). |
| `callback`       | Leave this value as `true` to indicate that this is the _Callbacks_ widget.                                                                                                                                                                                                                                                  |

### Callback Widget

#### Add Widget to Desktop Layout

To add the widget, add the following to your desktop layout JSON file, in the `agent > area > panel > children` section:

```json
{
  "comp": "md-tab",
  "attributes": {
    "slot": "tab"
  },
  "children": [
    {
      "comp": "img",
      "attributes": {
        "src": "https://velocity.customerdynamics.com/logo.svg",
        "height": 16,
        "width": 16
      }
    },
    {
      "comp": "span",
      "textContent": "Callback"
    }
  ]
},
{
  "comp": "md-tab-panel",
  "attributes": {
    "slot": "panel",
    "class": "widget-pane"
  },
  "children": [
    {
      "comp": "dynamic-area",
      "properties": {
        "area": {
          "id": "dw-panel-one",
          "widgets": {
            "cdyx-vel-callback": {
              "comp": "cdyx-vel-callback",
              "script": "https://velocity.customerdynamics.com/assets/callback.js",
              "attributes": {
                "dark": "$STORE.app.darkMode"
              },
              "properties": {
                "accessToken": "$STORE.auth.accessToken",
                "outdialEp": "$STORE.agent.outDialEp",
                "velocityApiKey": "",
                "velocityAuth": "",
                "agentId": "$STORE.agent.agentId",
                "teamId": "$STORE.agent.teamId",
                "agentName": "$STORE.agent.agentName",
                "callbackCreate": true
              }
            }
          },
          "layout": {
            "areas": [
              [
                "cdyx-vel-callback"
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
      }
    }
  ]
},
```

#### Define Widget Properties

Provide the appropriate values in the JSON above, using the following descriptions to guide you.

##### Script

The `script` to use for the widget depends on the environment used. For this value, use the URL that corresponds to your environment:

| Environment | Script URL                                                 |
| ----------- | ---------------------------------------------------------- |
| Development | `https://velocity-dev.cd-ccs.net/assets/callback.js`       |
| Staging     | `https://velocity-staging.cd-ccs.net/assets/callback.js`   |
| Production  | `https://velocity.customerdynamics.com/assets/callback.js` |

> [!NOTE]
> Unless otherwise specified for your tenant, use the production script.

##### General Configuration

Use the same values for `velocityApiKey`, and `velocityAuth` as you did for the previous widget. Leave the `callbackCreate` value as `true` to indicate that this is the _Callback_ widget.
