# arch-updater

**arch-updater** is a POSIX-compatible shell script designed for Arch Linux power users who demand absolute control over their system updates.

Unlike standard helpers that blindly update everything, this utility focuses on risk mitigation and stability. It allows you to granularly review changes, assess update risks based on package age and known issues, and segregate critical applications from system noise.

## Key Features

* **Unified Management:** Handle both official `pacman` repositories and AUR packages in a single view.
* **Selective Updates:** Cherry-pick exactly which packages to upgrade and which to hold back.
* **Risk Assessment:** Instantly gauge the stability of an update via package age indicators (filtering out "fresh" and potentially unstable packages) and open issue tracking.
* **Smart Categorization:** Separate packages into "Important" (apps you monitor) and "Unimportant" (libraries, deps) to reduce cognitive load.
* **Deep Insight:** View detailed changelogs, diffs, and warnings relative to your currently installed version before committing to an update.
* **Quick Links:** Jump directly to upstream URLs to check for breaking changes or new features.

## Screenshots

### Main Interface
![Main UI Screenshot](https://raw.githubusercontent.com/chpock/arch-updater/assets/screenshot-ui-changelog.png)
*The main view showing categorized packages, update status, and stability metrics.*

### Package Details & Issues
![Issues UI Screenshot](https://raw.githubusercontent.com/chpock/arch-updater/assets/screenshot-ui-issues.png)
*Detailed view showing specific issues and changelogs for a selected package.*

## Dependencies

This utility is a standalone shell script, but relies on the following tools:

**Required:**
* `pacman-contrib`: For the `checkupdates` utility.
* `yay`: For AUR package access.
* `fzf`: Drives the terminal user interface.

**Highly Recommended (for changelogs & metadata):**
* `curl`, `jq`, `expac`

**Optional:**
* `arch-log`: Enhanced changelog fetching for pacman/AUR.

## Installation

**arch-updater** can be installed as [AUR package](https://aur.archlinux.org/packages/arch-updater):

```shell
yay -S arch-updater
```

## Interface Guide

The UI is divided into three sections: the **Package List**, **Package details**, and **Keyboard shortcuts**.

### The Package List
This is your main workspace. Packages are visually separated to help you focus on what matters.

* **Categorization:**
    * **Bright White:** "Important" packages (e.g., main applications).
    * **Gray:** "Unimportant" packages (e.g., libraries, dependencies).
    * *Tip: Use `Ctrl-S` to toggle a package's category.*

* **Status Indicators:**
    * `[UPGR]`: Marked for upgrade.
    * `[SKIP]`: Will be held back (kept at current version).

* **Package origin:**
    * `[PAC]`: Official repository package.
    * `[AUR]`: Arch User Repository package.

* **Risk & Metadata Tags:**
    * **(X issues):** Indicates open issues exist for the new version.
    * **(age: X):** Shows how long the package has been in the repo.
        * *Note: only shown for packages less than 48 hours old. Old packages with no issues usually imply lower risk.*
    * **(dep):** Indicates the package was installed as a dependency, not explicitly.

### Package details
When a package is selected, the preview pane shows:
1.  **Metadata:** Standard package manager info.
2.  **Changelog:** A concise log of changes *specifically between your installed version and the new version*.
3.  **Issues:** A list of new issues reported since your currently installed version (if applicable).

## Controls

| Key | Action |
| :--- | :--- |
| **Space** | Toggle update status (Upgrade / Skip) |
| **Ctrl-S** | Toggle category (Important / Unimportant) |
| **Enter** | Open package URL (Check news/breaking changes) |
| **?** | Toggle Detail/Preview pane |
| **Ctrl-A** | Mark **ALL** packages for upgrade |
| **Ctrl-U** | Mark **ALL** packages to skip |
| **Alt-Enter** | **Execute Updates** (Apply changes) |
| **Esc / Ctrl-C** | Exit without updating |

## Workflow

1.  **Launch:** Run `arch-updater` in your terminal.
2.  **Review:** Scroll through the list.
    * Check for packages with low "Age" or "Issues" flagged.
    * Use **Space** to uncheck updates you deem risky or unnecessary.
    * Use **Ctrl-S** to categorize noise (libs) as unimportant for future runs.
3.  **Verify:** Read changelogs in the preview pane for critical packages.
4.  **Execute:** Press **Alt-Enter**.
    * The script will update official packages first.
    * AUR updates will follow.

## Copyright

Copyright (c) 2025 Konstantin Kushnir <chpock@gmail.com>
