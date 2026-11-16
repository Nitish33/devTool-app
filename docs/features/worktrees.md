# Worktrees

Create, open and clean up Git worktrees without leaving the app.

[← All features](../../README.md#features)

**On this page:** [Worktree list](#worktree-list) · [One-click IDE launch](#one-click-ide-launch) · [Search and keyboard navigation](#search-and-keyboard-navigation) · [Quick actions on each row](#quick-actions-on-each-row) · [Create a worktree](#create-a-worktree) · [Create from the clipboard](#create-from-the-clipboard) · [Deep links](#deep-links) · [Edit and delete](#edit-and-delete)

## Worktree list

Every worktree of the selected project, with its state visible at a glance.

- **Branch and folder:** each row shows the branch name with the folder path under it
- **Git status chips:** commits to pull, commits to push, staged files, changed files, conflicts, **local** when there is no upstream yet, and **clean**
- **Pull request status:** draft, review requested, approved, and the CI result
- **Jira status:** the state of the issue the branch belongs to
- **Size on disk:** how much space each worktree takes
- **Reorder:** drag rows into the order you want
- **Refresh:** one button reloads everything; status is read on refresh, with no background polling

![The main window with a project expanded, several worktrees, status chips, and PR and Jira badges visible](images/worktree-list.webp)

## One-click IDE launch

Click a worktree and it opens in your editor.

- **Editors:** VS Code, Cursor, Zed, JetBrains IDEs, or any custom command
- **Custom command:** write your own, using `{path}` for the worktree folder
- **Per-project editor:** a project can use a different editor from your default
- **Confirmation:** a dialog with the editor's icon, with **Don't ask again** to skip it from then on

![The IDE confirmation dialog with the editor icon and the Don't ask again option](images/ide-launch.webp)

## Search and keyboard navigation

Work through the list without touching the mouse.

- **Type to search** the worktrees
- **Arrow keys** move the highlight
- **Enter** opens the highlighted worktree
- **Esc** clears the search
- Forms and dialogs have keyboard shortcuts too

![The search field with a query typed, the list filtered, and one row highlighted](images/search.webp)

## Quick actions on each row

Hover a row to reach the things you do next.

- **Terminal:** open a terminal in the worktree
- **Finder:** reveal the folder
- **Xcode and Android Studio:** shown when the project has native iOS or Android folders
- **Run:** start the project's `start` script from `package.json` in a Terminal tab. If Metro is already on port 8081 it starts on the next free port, so a second branch never fights the first
- **Launch settings (gear):** change what Run, Xcode and Android Studio do for this worktree. See [Launch settings](#launch-settings)
- **Metro port:** a green `:8081` badge on the branch line shows which port the worktree's Metro is on, so with several projects running you can tell them apart
- **More actions:** edit or delete the worktree

![A hovered worktree row showing its action icons](images/quick-actions.webp)

## Launch settings

Run, Xcode and Android Studio often need setup first: the right Node version, a `PATH`, `JAVA_HOME`. Set it once instead of every time.

- **Gear icon on each worktree** opens a settings page (it scrolls, like Project Settings)
- **Before launching:** lines that run first, one per line, such as `nvm use 20` or `export JAVA_HOME=...`. They run in your login shell, and a failing line stops the rest, with the error shown on the row
- **Start, Android Studio and Xcode commands:** replace what the button does. Use `{path}` for the worktree folder and `{port}` for the Metro port. Leave a field empty to use the default, which is shown as its placeholder
- **Metro port:** a port to start on, when you want a fixed one
- **Defaults cascade:** the worktree's value, then the project's (in [Project settings](projects.md#project-settings)), then the built-in command. **Use default** clears one field and **Reset all** clears the page
- Android Studio and Xcode started from here get the setup's environment, so they open with the right Node and Java. An editor that is already running keeps the environment it had; quit it first

## Create a worktree

Start new work in its own folder in a few fields.

- **Base branch:** pick any local or remote branch to start from
- **Fetch before create:** pull the latest first, so you branch from fresh code
- **Branch name** built from an **issue number** and a short **description**
- **Folder:** generated for you from your path template, so worktrees stay tidy
- **Copy files:** bring files such as `.env` or config folders from the main repo into the new worktree
- **Auto-expand:** the new worktree appears straight away under its project

![The New Worktree form filled in, with the base branch menu open](images/create-worktree.webp)

## Create from the clipboard

Paste something you already have and let DevTool read the branch name from it.

- **Jira issue keys** such as `ABC-1234`
- **GitHub pull request URLs**
- **Your own patterns:** add regexes with named groups (`issueNumber`, `description`) for any other format
- Fills in the issue number and description, so the branch name follows your convention

![The create form with the branch name filled in from a pasted Jira key](images/create-from-clipboard.webp)

## Deep links

Create a worktree from outside the app.

- **`devtool://` links** open the create form from other tools, scripts or a browser
- **Branch parameter** to pre-fill the branch
- Useful for a button in a ticket, a chat bot or a shell alias

![A terminal or browser running a devtool:// link next to the create form it opened](images/deep-links.webp)

## Edit and delete

Tidy up when the work is done.

- **Rename the branch** and edit the description and issue number (the main branch can't be renamed)
- **Delete a worktree** with a confirmation that shows progress
- **Also delete the local branch** with one checkbox, so no orphaned branches pile up
- **Force delete:** if the worktree has local changes you are told why and asked before it is removed

![The delete confirmation with the Also delete local branch option](images/edit-delete.webp)
