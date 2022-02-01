# 💻 Dotfiles

Migrating to a new Mac is a pain. To alleviate that, this repository automates a bunch of the steps involved so there's way less to do manually. Forked from [driesvints/dotfiles](https://github.com/driesvints/dotfiles) (handy [blog post](https://driesvints.com/blog/getting-started-with-dotfiles)) - thanks Dries.

### How it works

* **[Homebrew](https://brew.sh/) + Homebrew Bundle** - does the heavy lifting. Homebrew Bundle installs the resources listed in the accompanying Brewfile, using one of the following commands:
  * tap - a repository of formulae (things to install)
  * brew - a binary to install, e.g. git
  * cask - a MacOS app to install, e.g. Figma *<= most apps are installed this way*
  * mas - an AppStore app to install
* **.zshrc** - handy shell settings
* **[Mackup](https://github.com/lra/mackup)** - synchronises app settings to Dropbox
* **.macos** - shell script configuration file that sets a bunch of system settings & preferences, e.g. hot-corners, scroll preferences, etc.

# Fresh macOS setup

Assuming your dotfiles are already set up, start here. (Instructions on setting dotfiles for the first time are [below](#roll-your-own).)

## On your old machine

- Commit and push any changes/branches to your git repositories
- Save all important documents from non-iCloud/Dropbox directories
- Export data from any local databases
- Update [mackup](https://github.com/lra/mackup) to the latest version - `brew upgrade mackup` - and run `mackup backup`

## On your new machine

1. If your 'new' machine is actually a macOS re-install over your old machine follow [these steps](https://www.imore.com/how-do-clean-install-macos).
2. Update macOS to the latest version with the App Store
3. Git clone this repo to `~/.dotfiles`
4. Install X-Code command-line tools (might already be handled by the previous step):

    ```
    touch /tmp/.com.apple.dt.CommandLineTools.installondemand.in-progress;
    softwareupdate -i -a
    rm /tmp/.com.apple.dt.CommandLineTools.installondemand.in-progress
    ```

5. Copy your public and private SSH keys to `~/.ssh` and make sure they're set to `600`
6. [Grant full disk access](https://github.com/mathiasbynens/dotfiles/issues/849#issuecomment-436099833) to Terminal and/or iTerm so that it can actually update OS / application preferences using the `defaults` command.
7. Run `install.sh` to start the installation
8. Login to Dropbox and get it sync-ing. Mackup needs Dropbox available to read the backed-up application settings.
9.  Restore preferences by running `mackup restore`

At this point all the dotfile wizardry is complete. You now have to resume the tedious mop-up of manual steps...

1. Restart your computer and launch all the apps you've just installed. Click lots of 'I accept' buttons.
2. **Firefox** - [Backup and restore your current profile](https://support.mozilla.org/en-US/kb/back-and-restore-information-firefox-profiles).
3. **Chrome** - [Chrome automatically syncs](https://support.google.com/chrome/answer/185277) tabs, extensions, etc between different Chrome instances. Restoring tabs doesn't happen automagically between machines though (which kinda makes sense to be fair). To restore tabs in the new Chrome instance go to  
*History* (⌘Y) *> Tabs from other devices* (top left menu) *> Dots* (top right menu) *> Open all*.
1. Enable email accounts (System preferences > Internet accounts) and start syncing email.
2. Set desktop backgrounds and screensaver ([Aerial](https://aerialscreensaver.github.io/) is awesome).
3. Install hardware drivers, e.g. RME Babyface

# Roll your own

If you want to start with your own dotfiles from this setup, it's pretty easy to do so. First of all you'll need to fork this repo. After that you can tweak it the way you want.

The instructions below assume you already have set up Oh My Zsh so make sure to first [install Oh My Zsh](https://github.com/robbyrussell/oh-my-zsh#getting-started) before you continue.

Go through the [`.macos`](./.macos) file and adjust the settings to your liking. You can find much more settings at [the original script by Mathias Bynens](https://github.com/mathiasbynens/dotfiles/blob/master/.macos) and [Kevin Suttle's macOS Defaults project](https://github.com/kevinSuttle/MacOS-Defaults).

Check out the [`Brewfile`](./Brewfile) file and adjust the apps you want to install for your machine. Use [their search page](https://caskroom.github.io/search) to check if the app you want to install is available.

Check out the [`aliases.zsh`](./aliases.zsh) file and add your own aliases. If you need to tweak your `$PATH` check out the [`path.zsh`](./path.zsh) file. These files get loaded in because the `$ZSH_CUSTOM` setting points to the `.dotfiles` directory. You can adjust the [`.zshrc`](./.zshrc) file to your liking to tweak your Oh My Zsh setup. More info about how to customize Oh My Zsh can be found [here](https://github.com/robbyrussell/oh-my-zsh/wiki/Customization).

When installing these dotfiles for the first time you'll need to backup all of your settings with Mackup. Install Mackup and backup your settings with the commands below. Your settings will be synced to iCloud so you can use them to sync between computers and reinstall them when reinstalling your Mac. If you want to save your settings to a different directory or different storage than iCloud, [checkout the documentation](https://github.com/lra/mackup/blob/master/doc/README.md#storage).

```zsh
brew install mackup
mackup backup
```

You can tweak the shell theme, the Oh My Zsh settings and much more. Go through the files in this repo and tweak everything to your liking.

Enjoy your own Dotfiles!

______

## Thanks

I first got the idea for starting this project by visiting the [Github does dotfiles](https://dotfiles.github.io/) project. Both [Zach Holman](https://github.com/holman/dotfiles) and [Mathias Bynens](https://github.com/mathiasbynens/dotfiles) were great sources of inspiration. [Sourabh Bajaj](https://twitter.com/sb2nov/)'s [Mac OS X Setup Guide](http://sourabhbajaj.com/mac-setup/) proved to be invaluable. Thanks to [Taylor Otwell](https://twitter.com/taylorotwell) for his awesome Zsh theme! And lastly, I'd like to thank [Maxime Fabre](https://twitter.com/anahkiasen) for [his excellent presentation on Homebrew](https://speakerdeck.com/anahkiasen/a-storm-homebrewin) which made me migrate a lot to a [`Brewfile`](./Brewfile) and [Mackup](https://github.com/lra/mackup).

In general, I'd like to thank every single one who open-sources their dotfiles for their effort to contribute something to the open-source community. Your work means the world! :earth_africa: :heart:
