# Nested Flows

If you'd like to avoid duplication of code or otherwise modularize your Flow files, you can use the `runFlow` command to run commands from another file.

### runFlow

Runs a flow from a specified file:

```yaml
- runFlow: anotherFlow.yaml
```

#### Run flows conditionally

Sometimes you'd want to run flows only under certain conditions. Check out more in the page below

{% content-ref url="conditions.md" %}
[conditions.md](conditions.md)
{% endcontent-ref %}

#### Example

Let's say you have a login sequence that you'd like to reuse across multiple flows. You can write the login commands in a separate file and run those steps from another Flow:

{% tabs %}
{% tab title="Login.yaml" %}
```yaml
appId: com.example.app
---
- launchApp
- tapOn: Username
- inputText: Test User
- tapOn: Password
- inputText: Test Password
- tapOn: Login
```
{% endtab %}

{% tab title="Profile.yaml" %}
```yaml
appId: com.example.app
---
- runFlow: Login.yaml # <-- Run commands from "Login.yaml"
- tapOn: Profile
- assertVisible: "Name: Test User"
```
{% endtab %}

{% tab title="Settings.yaml" %}
```yaml
appId: com.example.app
---
- runFlow: Login.yaml # <-- Run commands from "Login.yaml"
- tapOn: Settings
- assertVisible: "Switch to dark mode"
```
{% endtab %}
{% endtabs %}