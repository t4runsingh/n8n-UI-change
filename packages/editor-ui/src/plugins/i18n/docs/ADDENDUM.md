# Addendum for i18n in n8n

## Base text

### Interpolation

Certain base text strings use [interpolation](https://kazupon.github.io/vue-i18n/guide/formatting.html#named-formatting) to allow for a variable to be passed in, signalled by curly braces:

```json
{
	"stopExecution": {
		"message": "The execution with the ID {activeExecutionId} got stopped!",
		"title": "Execution stopped"
	}
}
```

When translating a string containing an interpolated variable, leave the variable untranslated:

```json
{
	"stopExecution": {
		"message": "Die AusfΓΌhrung mit der ID {activeExecutionId} wurde gestoppt",
		"title": "Execution stopped"
	}
}
```

### Reusable base text

As a convenience, the base text file may contain the special key `reusableBaseText`, which defines strings that can be shared among other strings with the syntax `@:reusableBaseText.key`, as follows:

```json
{
	"reusableBaseText": {
		"save": "π©πͺ Save",
	},
	"duplicateWorkflowDialog": {
		"enterWorkflowName": "π©πͺ Enter workflow name",
		"save": "@:reusableBaseText.save",
	},
	"saveButton": {
		"save": "@:reusableBaseText.save",
		"saving": "π©πͺ Saving",
		"saved": "π©πͺ Saved",
	},
}
```

For more information, refer to Vue i18n's [linked locale messages](https://kazupon.github.io/vue-i18n/guide/messages.html#linked-locale-messages).

### Nodes in versioned dirs

For nodes in versioned dirs, place the `/translations` dir for the node translation file alongside the versioned `*.node.ts` file:

```
Mattermost
  βββ Mattermost.node.ts
    βββ v1
        βββ MattermostV1.node.ts
        βββ actions
        βββ methods
        βββ transport
        βββ translations
            βββ de
                βββ mattermost.json
```

### Nodes in grouping dirs

For nodes in grouping dirs, e.g. Google nodes, place the `/translations` dir for the node translation file alongside the `*.node.ts` file:

```
Google
  βββ Books
  βββ Calendar
  βββ Drive
      βββ GoogleDrive.node.ts
      βββ translations
          βββ de
              βββ googleDrive.json
              βββ googleDriveTrigger.json
```

## Dynamic text

### Reusable dynamic text

The base text file may contain the special key `reusableDynamicText`, allowing for a node parameter to be translated once and reused in all other node parameter translations.

Currently only the keys `oauth.clientId` and `oauth.clientSecret` are supported as a PoC - these two translations will be reused in all node credential parameters.

```json
{
	"reusableDynamicText": {
		"oauth2": {
			"clientId": "π©πͺ Client ID",
			"clientSecret": "π©πͺ Client Secret",
		}
	}
}
```

### Special cases

`eventTriggerDescription` is a dynamic node property that is not part of node parameters. To translate it, set the `eventTriggerDescription` key at the root level of the `nodeView` property in the node translation file.

```json
{
	"nodeView": {
		"eventTriggerDescription": "π©πͺ Waiting for you to call the Test URL"
	}
}
```
