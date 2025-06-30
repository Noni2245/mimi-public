# Discord Bot Self-Role Selector Guide

This detailed guide explains how to use the advanced self-role selector feature in your Discord bot, including associating custom messages with each role option.

---

## Table of Contents

1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Admin Setup: Creating a Role Selector Embed](#admin-setup-creating-a-role-selector-embed)
    - [Command Syntax](#command-syntax)
    - [Example Usage](#example-usage)
    - [Supported Emojis](#supported-emojis)
4. [How Users Assign/Remove Roles](#how-users-assignremove-roles)
5. [How It Works](#how-it-works)
6. [Persistence and Data Storage](#persistence-and-data-storage)
7. [Troubleshooting and Tips](#troubleshooting-and-tips)
8. [FAQ](#faq)
9. [Customization Ideas](#customization-ideas)

---

## Overview

The self-role selector lets server members assign or remove roles from themselves by reacting to a special message (embed) with specific emojis. The server admin can configure which emojis map to which roles and include a **custom message for each emoji/role pair**. This setup is persistent across bot restarts.

---

## Prerequisites

- The bot must have the following permissions:
    - **Manage Roles**
    - **Read Messages**
    - **Send Messages**
    - **Add Reactions**
    - **Read Message History**
- The roles you want to assign **must be below the bot's highest role** in the server's role hierarchy.
- The server admin’s Discord user ID must be set in the `.env` file as `ADMIN_ID`.

---

## Admin Setup: Creating a Role Selector Embed

Only the admin (as set by `ADMIN_ID` in `.env`) can run the setup command.

### Command Syntax

```
!rolesetup #channel EMOJI @Role "Message" EMOJI @Role "Message" ...
```
- `#channel` — the channel you want the embed posted in.
- `EMOJI` — the emoji to use for assignment (Unicode or custom).
- `@Role` — mention the role (type `@rolename` and select from the popup).
- `"Message"` — a custom message/description for this emoji-role pair (must be in double quotes).

Each emoji/role/message group is parsed in the order given.

### Example Usage

Suppose you want users to pick between "Red Team" and "Blue Team" roles using 🟥 and 🟦, with custom instructions.

1. Ensure roles "Red Team" and "Blue Team" exist in your server.
2. In any channel, as the admin, type:

    ```
    !rolesetup #roles 🟥 @Red\ Team "Click to get the red team role" 🟦 @Blue\ Team "Click to get the blue team role"
    ```

    (If your role names have spaces, type `@Red Team` and select from the popup; Discord will format as `<@&roleid>`.)

3. The bot will post an embed in #roles like:

    ```
    🟥 @Red Team — Click to get the red team role
    🟦 @Blue Team — Click to get the blue team role
    ```

    The embed will have a **blue accent line**.

4. The bot adds the corresponding emoji reactions automatically.

### Supported Emojis

- **Standard Unicode emojis:** e.g., 🟥, 🟦, 😃, 👍
- **Custom server emojis:** use the emoji exactly as it appears in Discord (e.g., `<:customemoji:1234567890>`)

---

## How Users Assign/Remove Roles

**Assigning:**
- Click the emoji under the role selector message.
- The bot will give you the corresponding role.

**Removing:**
- Remove your reaction.
- The bot will remove the corresponding role.

Users can have multiple roles if they react to multiple emojis.

---

## How It Works

- When the admin runs `!rolesetup`, the bot:
    - Posts an embed listing all emoji/role/message pairs.
    - Adds each mapped emoji as a reaction.
    - Saves the mapping (including custom messages) in a `roleEmbeds.json` file for persistence.

- When a user reacts/un-reacts:
    - The bot checks if the reaction is on a role selector embed.
    - If so, it adds or removes the corresponding role from the user.

- The mapping persists across bot restarts.

---

## Persistence and Data Storage

- The emoji-role-message mapping for each selector message is stored in a file called `roleEmbeds.json` in the bot directory.
- Do **not** delete this file unless you want to reset all mappings.
- If you delete the setup message in Discord, the mapping remains, but the message will no longer function for role assignment.

---

## Troubleshooting and Tips

- **Bot doesn’t react or assign roles:**  
    - Check the bot’s permissions (see [Prerequisites](#prerequisites)).
    - Make sure the roles are below the bot’s highest role.
    - Make sure you used the correct role mentions.

- **Custom emoji not working:**  
    - The bot must have access to the emoji (it’s from the same server or a server the bot is in).
    - Use the emoji code as it appears in Discord.

- **Roles not removed when reaction is removed:**  
    - Ensure the bot has "Manage Roles" permission.
    - Ensure the bot is running and online.

- **Bot restarts and role selector stops working:**  
    - If you moved or deleted `roleEmbeds.json`, the mapping is lost. Recreate the selector.

---

## FAQ

**Q: Can I use the same emoji for multiple roles?**  
A: No, each emoji can only map to one role per message.

**Q: Can I create multiple role selector messages?**  
A: Yes! Each message has its own mapping and works independently.

**Q: Can users assign themselves roles not listed in the selector?**  
A: No, only the roles mapped in the embed can be self-assigned via reactions.

**Q: Can anyone run `!rolesetup`?**  
A: No, only the Discord user whose ID is set as `ADMIN_ID` in the `.env` can run this command.

---

## Customization Ideas

- Require only one role at a time (remove previous role when a new one is chosen).
- Allow admins to remove or edit mappings via commands.
- Use buttons/select menus (Discord component API) for role assignment (advanced).
- Log role assignments/removals for moderation.

---

## Need More Help?

If you encounter issues not covered here, check:
- The bot console/logs for error messages.
- That your `.env` and `roleEmbeds.json` files are configured correctly.
- Discord permissions for your bot and roles.

Happy role assigning!
