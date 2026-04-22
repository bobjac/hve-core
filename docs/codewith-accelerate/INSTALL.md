# Code With Accelerate: Build and Install Guide

Build the Code With Accelerate VS Code extension from source and distribute it to your team without publishing to the VS Code Marketplace.

## Prerequisites

| Requirement | Version | Install |
|-------------|---------|---------|
| Node.js | 20+ | [nodejs.org](https://nodejs.org) |
| PowerShell | 7+ | [Install PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell) |
| PowerShell-Yaml module | Any | `Install-Module -Name PowerShell-Yaml -Force -Scope CurrentUser` |
| Git | Any | [git-scm.com](https://git-scm.com) |

## Build the Extension

### 1. Clone the repository

```bash
git clone https://github.com/bobjac/hve-core.git
cd hve-core
```

### 2. Install dependencies

```bash
npm ci
```

### 3. Prepare the extension

This step discovers the Code With Accelerate artifacts from the collection manifest and generates `extension/package.json`.

```bash
pwsh ./scripts/extension/Prepare-Extension.ps1 \
  -Channel PreRelease \
  -Collection collections/codewith-accelerate.collection.yml
```

You should see output confirming the discovered artifacts:

```
Agents: 3
Prompts: 6
Instructions: 4
Skills: 3
```

> [!NOTE]
> The `-Channel PreRelease` flag is required because Code With Accelerate artifacts use `preview` maturity. The Stable channel only includes `stable` maturity artifacts.

### 4. Package the extension

This step copies the filtered artifacts into `extension/`, runs `vsce package`, and produces a `.vsix` file.

```bash
pwsh ./scripts/extension/Package-Extension.ps1 \
  -Collection collections/codewith-accelerate.collection.yml \
  -PreRelease
```

The output `.vsix` file is created in the `extension/` directory:

```
extension/hve-codewith-accelerate-3.3.41.vsix
```

## Install the Extension

### Option A: VS Code UI

1. Open VS Code (or VS Code Insiders).
2. Press `Cmd+Shift+P` (macOS) or `Ctrl+Shift+P` (Windows/Linux).
3. Type "Extensions: Install from VSIX..." and select it.
4. Navigate to the `.vsix` file and select it.
5. Reload the window when prompted (`Cmd+Shift+P` > "Developer: Reload Window").

### Option B: Command line

```bash
# VS Code
code --install-extension extension/hve-codewith-accelerate-3.3.41.vsix

# VS Code Insiders
code-insiders --install-extension extension/hve-codewith-accelerate-3.3.41.vsix
```

> [!TIP]
> If the `code` or `code-insiders` command is not found, open VS Code and run `Cmd+Shift+P` > "Shell Command: Install 'code' command in PATH".

### Verify installation

After reloading, open the Copilot Chat panel and type `@`. You should see **Code With Accelerate** in the agent list.

## Distribute to Your Team

The `.vsix` file is a self-contained package that anyone can install. No Marketplace account or publishing step is needed.

### Share via file transfer

1. Build the `.vsix` using the steps above.
2. Share the `hve-codewith-accelerate-3.3.41.vsix` file with your team via:
   - SharePoint / OneDrive
   - Teams file sharing
   - Secure file transfer
   - GitHub Release (attach as an asset to a release on your fork)
3. Each team member installs using Option A or Option B above.

### Share via GitHub Release

Create a release on your fork and attach the `.vsix` as an asset:

```bash
# Tag and create a release
git tag -a v3.3.41-codewith-accelerate -m "Code With Accelerate extension"
git push origin v3.3.41-codewith-accelerate

# Create a GitHub release and attach the .vsix
gh release create v3.3.41-codewith-accelerate \
  extension/hve-codewith-accelerate-3.3.41.vsix \
  --title "Code With Accelerate v3.3.41" \
  --notes "VS Code extension for constitution generation and PoC integration workflows."
```

Team members download from the Releases page and install the `.vsix` locally.

## Updating the Extension

When you make changes to the agent, prompts, instructions, or skills:

1. Edit the source files under `.github/` in the repository.
2. Rebuild the `.vsix` (steps 3 and 4 above).
3. Install the new `.vsix` directly over the existing one (no need to uninstall first, unless the agent name changed).
4. Reload VS Code.

> [!IMPORTANT]
> If you change the agent `name` field in the frontmatter, uninstall the old extension before installing the new one. VS Code may cache the old name otherwise.

## Uninstalling

### VS Code UI

1. `Cmd+Shift+P` > "Extensions: Show Installed Extensions"
2. Search for "CodeWith" or "HVE"
3. Click **Uninstall** on "HVE Core - CodeWith Accelerate"
4. Reload the window

### Command line

```bash
code --uninstall-extension ise-hve-essentials.hve-codewith-accelerate
```

## Coexistence with HVE Core

Code With Accelerate installs alongside the HVE Core extension without conflicts. They have separate extension IDs:

| Extension | ID |
|-----------|-----|
| HVE Core (Marketplace) | `ise-hve-essentials.hve-core-all` |
| Code With Accelerate (sideloaded) | `ise-hve-essentials.hve-codewith-accelerate` |

Both can be installed and active simultaneously.

## What's Included

The extension packages these artifacts:

| Type | Count | Contents |
|------|-------|----------|
| Agents | 3 | Code With Accelerate orchestrator, Constitution Researcher subagent, PoC Integrator subagent |
| Prompts | 6 | gen-constitution, gen-constitution-feature, gen-poc-plan, integrate-poc, deliver-constitution, constitution-continue |
| Instructions | 4 | Constitution conventions, PoC integration standards, privacy constraints, HVE core location |
| Skills | 3 | Proprietary screening, constitution validation, PR reference |

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Agent not showing in Copilot Chat | Reload the window. If still missing, uninstall and reinstall the `.vsix`. |
| Duplicate agents in the list | You have both the extension and a local `.github/agents/` file in the workspace. Delete the local file or disable the extension for that workspace. |
| `Prepare-Extension.ps1` shows 0 agents | You forgot `-Channel PreRelease`. The artifacts are `preview` maturity, which requires the PreRelease channel. |
| `PowerShell-Yaml` not found | Run `Install-Module -Name PowerShell-Yaml -Force -Scope CurrentUser` in PowerShell. |
| `vsce` not found | Run `npm ci` first to install dev dependencies. The scripts use `npx vsce` automatically. |
