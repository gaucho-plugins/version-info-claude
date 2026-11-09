# Version Info

**Inventory server software** · [Gaucho Plugins](https://gauchoplugins.com/)

Find which servers run a particular PHP, Node.js, or Python version. Look up installed packages, plugins, and themes, see what changed, and check when each server last reported.

This plugin connects Claude to your Version Info account. It contains one setup skill and one remote MCP connection. The service runs separately; no server program, local hook, or credential is included in this package.

## What you can inspect

- **Ubuntu/Debian x86-64 hosts:** operating system, kernel, installed Debian packages, and PHP, Node.js, and Python runtimes available in supported system locations.
- **WordPress sites:** core, plugins, themes, PHP and available extension versions, plus database and web-server information when available.
- **Observed changes:** additions, removals, and version changes between successful reports during the last seven days.
- **Report status:** when the server last reported successfully, what was covered, and which values are only last known.

The free account supports three environments. One site or Linux host uses one slot; connecting both on one machine uses two. The first report follows approved setup. Subsequent reports are scheduled hourly; WordPress scheduling depends on site traffic. Installed versions are reported as provided by the source, including distribution-specific package revisions.

This release does not scan application dependencies or Docker, compare versions with the latest public releases, assess vulnerabilities, send notifications, or perform upgrades.

## Connect in Claude

1. Add **Version Info** in **Customize → Plugins**. Open its **Connectors** tab and add or connect Version Info.
2. Sign in on Version Info's website with your email and emailed code, then approve the Claude connection. A free account is created after verification. Use the same email to access an existing account and its servers.
3. Ask **“Help me connect a Linux server or WordPress site.”** The setup skill retrieves the current instructions and download availability.
4. Complete the server setup yourself, then ask **“Show my connected servers.”**

Installing the Claude plugin does not authorize your account or install software on your servers. WordPress setup begins on the Version Info website and uses a separate optional integration; the main WordPress plugin is not required. Linux setup uses the existing server user's permissions and requires browser approval. On Claude Team or Enterprise, an organization owner may need to add the connector first.

The plugin's skills and connector are available in Claude web, desktop, and mobile chats. A plugin enabled on your Claude account also syncs to supported Claude Code versions when you sign in with that account. In Code, use `/mcp` to finish the Version Info sign-in if requested and `/reload-plugins` after a plugin sync. Command-line installations do not install the plugin on your Claude web account.

## Questions to try

- “Help me connect a Linux server or WordPress site.”
- “Show software versions across my connected servers.”
- “Which servers run PHP?”
- “What changed on my servers this week?”

You can also request a server rename. To disconnect a server, ask for its disconnect link and confirm on the website. Disconnecting removes its stored inventory and observed changes; revoking Claude's authorization is a separate account-connection action.

## Claude Code troubleshooting

Use the plugin's existing Version Info entry in `/mcp` first. Do not create another entry when that one works. Sign in through the browser; no client secret is required or supplied by this package.

If you need a standalone Code connection instead of the bundled one, this command registers the same endpoint with a public client ID and the required scopes:

```sh
claude mcp add-json version-info '{"type":"http","url":"https://mcp.versioninfoplugin.com/claude/mcp","oauth":{"clientId":"versioninfo-claude-code","scopes":"openid email offline_access inventory:read connections:write"}}' --scope user
```

Then use `/mcp` to authenticate. The client ID is a public identifier, not a password. Keep the endpoint exactly as shown so Claude Code can recognize duplicate server definitions. A standalone entry takes precedence over a plugin or account-synced connection; it does not provide the setup skill by itself.

## Help and data handling

[Setup guide](https://app.versioninfoplugin.com/claude) · [Support](https://gauchoplugins.com/support/) · [Cloud privacy policy](https://app.versioninfoplugin.com/privacy) · [Cloud terms](https://app.versioninfoplugin.com/terms)

Approved servers send software-version metadata to Version Info. Claude receives the reports you request through your authorized account. Never put passwords, email codes, SSH keys, or upload credentials in a chat or support request.

## Package validation

Use a current Claude Code release (this package was validated with 2.1.318) to validate locally without running a model:

```sh
claude plugin validate --strict --profile directory .
```

The package is independently versioned from the Version Info WordPress plugin and the ChatGPT package. Source instructions and configuration are MIT licensed; the name, logo, and other branding are excluded as described in [LICENSE](LICENSE).
