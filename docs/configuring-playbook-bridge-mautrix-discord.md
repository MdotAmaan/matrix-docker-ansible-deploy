# Setting up Mautrix Discord (optional)

**Note**: bridging to [Discord](https://discordapp.com/) can also happen via the [mx-puppet-discord](configuring-playbook-bridge-mx-puppet-discord.md) and [matrix-appservice-discord](configuring-playbook-bridge-appservice-discord.md) bridges supported by the playbook.

The playbook can install and configure [mautrix-discord](https://github.com/mautrix/discord) for you.

See the project's [documentation](https://docs.mau.fi/bridges/go/discord/index.html) to learn what it does and why it might be useful to you.

Use the following playbook configuration:

```yaml
matrix_mautrix_discord_enabled: true
``` 

## Set up Double Puppeting

If you'd like to use [Double Puppeting](https://docs.mau.fi/bridges/general/double-puppeting.html) (hint: you most likely do), you have 2 ways of going about it.

### Method 1: automatically, by enabling Shared Secret Auth

The bridge will automatically perform Double Puppeting if you enable [Shared Secret Auth](configuring-playbook-shared-secret-auth.md) for this playbook.

This is the recommended way of setting up Double Puppeting, as it's easier to accomplish, works for all your users automatically, and has less of a chance of breaking in the future.

### Method 2: manually, by asking each user to provide a working access token

**Note**: This method for enabling Double Puppeting can be configured only after you've already set up bridging (see [Usage](#usage)).

When using this method, **each user** that wishes to enable Double Puppeting needs to follow the following steps:

- retrieve a Matrix access token for yourself. You can use the following command:

```
curl \
--data '{"identifier": {"type": "m.id.user", "user": "YOUR_MATRIX_USERNAME" }, "password": "YOUR_MATRIX_PASSWORD", "type": "m.login.password", "device_id": "Mautrix-Discord", "initial_device_display_name": "Mautrix-Discord"}' \
https://matrix.DOMAIN/_matrix/client/r0/login
```

- send the access token to the bot. Example: `login-matrix MATRIX_ACCESS_TOKEN_HERE`

- make sure you don't log out the `Mautrix-Discord` device some time in the future, as that would break the Double Puppeting feature

## Usage

You then need to start a chat with `@discordbot:YOUR_DOMAIN` (where `YOUR_DOMAIN` is your base domain, not the `matrix.` domain).
