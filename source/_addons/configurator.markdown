---
layout: page
title: "HASS Configurator"
description: "Browser-based configuration file editor for Home Assistant."
date: 2017-09-25 14:00
sidebar: true
comments: false
sharing: true
footer: true
featured: true
og_image: /images/hassio/screenshots/addon-hass-configurator.png
---

As long as a fully featured configuration GUI for Home Assistant is still under development, you can use this add-on to add a browser based file-editor to your Hass.IO installation. By default it will listen on port `3218` of the host Hass.IO is running on.

More information and a standalone version for regular Home Assistant installations can be found in the [GitHub repository][code].

[code]: https://github.com/danielperna84/hass-configurator

<p class='img'>
<img src='/images/hassio/screenshots/addon-hass-configurator.png'>
Screenshot of the HASS Configurator.
</p>

### {% linkable_title Feature list %}

- Web-Based editor to modify your files with syntax highlighting.
- Upload and download files.
- Stage and commit changes in Git repositories, create and switch between branches, push to remotes.
- Lists of available triggers, events, entities, conditions and services. Selected element gets inserted into the editor at the last cursor position.
- Restart Home Assistant directly with the click of a button. Reloading groups, automations etc. can be done as well. An API-password is required.
- SSL support.
- Optional authentication and IP filtering for added security.
- Direct links to Home Assistant documentation and icons.
- Execute shell commands within the add-on container.
- Editor settings are saved in your browser.

### {% linkable_title Add-on Configuration %}

```json
{
  "homeassistant_api": "http://homeassistant:8123/api",
  "homeassistant_password": "",
  "username": "admin",
  "password": "secret",
  "certfile": "fullchain.pem",
  "keyfile": "privkey.pem",
  "ssl": false,
  "allowed_networks": ["192.168.0.0/16"],
  "banned_ips": ["8.8.8.8"],
  "ignore_pattern": ["__pycache__"]
}
```

- **homeassistant_api** (*Optional*): The configurator fetches some data from your running Home Assistant instance. If the API is not available through the default URL, modify this variable to fix this.
- **homeassistant_password** (*Optional*): If you plan on using API functions, you have to set your API password. Calling services of Home Assistant is prohibited without authentication.
- **username** (*Optional*): Set a username to access your configuration is protected.
- **password** (*Required*): Set a password for access.
- **ssl** (*Optional*): Enable or Disable SSL for the editor.
- **allowed_networks** (*Optional*): Limit access to the configurator by adding allowed IP addresses / networks to the list.
- **banned_ips** (*Optional*): List of statically banned IP addresses.
- **ignore_pattern** (*Optional*): Files and folders to ignore in the UI.

### {% linkable_title Embedding into Home-Assistant %}

Using the Home Assistant component [panel_iframe](https://home-assistant.io/components/panel_iframe/) it is possible to embed the configurator directly into Home Assistant, allowing you to modify your configuration within the Home Assistant frontend.

An example configuration would look like this:

```yaml
panel_iframe:
  configurator:
    title: Configurator
    icon: mdi:wrench
    url: http://hassio.local:3218
```

<p class='note warning'>
Be careful when setting up port forwarding to the configurator while embedding into Home Assistant. If you don't restrict access by requiring authentication and / or blocking based on client IP addresses, your configuration will be exposed to the internet!
</p>
