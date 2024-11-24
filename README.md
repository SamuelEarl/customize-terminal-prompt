# Customize Terminal Prompt

_Source: [How to spice up your Linux (Ubuntu) terminal prompt (using powerlevel10k and oh-my-zsh) in 2021](https://www.youtube.com/watch?v=PZTLIVQxxEY)_

The Bourne-Again shell (bash) is the default shell in Ubuntu. Z shell (Zsh) is an extended bash shell with many improvements.

## Install Z shell

```
sudo apt install zsh
```

## Change default shell

Check your shell:

```
echo $0
```

This should return `bash`.

Change shell:

```
chsh
```

Enter your password, then at the prompt that says `Login Shell [/bin/bash]:` enter `/bin/zsh`

Then restart you computer to enable Zsh.

After your computer restarts, open your terminal and you will see a message from Zsh to create a startup file (e.g. `.zshrc`). Type `2` to create a `.zshrc` file.

Confirm that you are in Zsh:

```
echo $0
```

You should see `zsh`.


## Install Oh My Zsh

Go to https://ohmyz.sh/, click the "Install oh-my-zsh" button, and run the `curl` command to install Oh My Zsh.

## Clone the powerlevel10 theme for Oh My Zsh

Go to https://github.com/romkatv/powerlevel10k?tab=readme-ov-file#oh-my-zsh where you can find this command:

```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

Copy and paste that into your Home directory.

## Install fonts for powerlevel10 theme

Clone this repo to your Home directory: 

```
git clone https://github.com/SamuelEarl/my-linux-setup
```

Create a `.fonts` directory in your Home directory and copy/paste the fonts from the `my-linux-setup/powerline-fonts` directory into the `.fonts` directory.

## Configure fonts for powerlevel10 theme

1. Open your terminal settings by clicking the menu icon >> "Preferences".
2. Select your profile.
3. Check the box next to "Custom font"
4. Click the font name button and search for "MesloLGS NF".
5. Click "Select".
6. Close the terminal "Preferences" window.

If the font in your terminal window looks weird, close your terminal and open it again. The font should look normal now.

## Update theme setting

Open your `.zshrc` file and change `ZSH_THEME="robbyrussell"` to `ZSH_THEME="powerlevel10k/powerlevel10k"`.

Close all terminal windows and open a new terminal window. You should now see the "Powerlevel10k configuration wizard" in your terminal. Follow the prompts to configure your terminal.

## Change Powerlevel10k configs

You can run `p10k configure` start the "Powerlevel10k configuration wizard" again or edit the `~/.p10k.zsh` file.

## Add Anaconda and conda to Zsh

Run this command to initialize conda:

```
~/anaconda3/bin/conda init zsh
```

NOTE: If your `anaconda3` directory is located somewhere else, then use that file path.

Restart your zsh shell to enable conda. The init command will change your `~/.zshrc` file accordingly, setting your `PATH` correctly and changing the PS1 to include the current conda environment.

## How to get Zsh configs to appear in VS Code terminal

Go to https://github.com/ryanoasis/nerd-fonts/releases/latest, scroll down to "Assets", and find the "Meslo.zip" file. Click the "Meslo.zip" link to download the fonts.

Unzip/extract the contents of the "Meslo.zip" file.

Move the unzipped folder to `/usr/share/fonts/truetype/`:

```
sudo mv ~/Downloads/Meslo /usr/share/fonts/truetype
```

Run this command to scan the font directories and configure fonts for use:

```
sudo fc-cache -vf /usr/share/fonts/
```

In VS Code, open File >> Preferences >> Settings and search for `terminal.integrated.fontFamily`. Set the font name you copied at the previous step into the `Terminal › Integrated: Font Family` field: `MesloLGS NF`

You can verify this setting in the `settings.json` file (Preferences >> Profiles >> Settings). You should see a line like this:

```json
"terminal.integrated.fontFamily": "MesloLGS NF"
```

Make sure that your settings.json file is saved. You will probably have to restart your computer to see the changes in your VS Code terminal.

```
"terminal.integrated.fontFamily": "MesloLGS NF"
```

_Source: https://stackoverflow.com/questions/62710890/font-issues-while-integrating-zsh-on-visual-studio-code_

## Characters at the end of my Powerlevel10k prompt

[What do characters like !1 at the end of my Powerlevel10k prompt mean?](https://stackoverflow.com/questions/62072056/what-do-characters-like-1-at-the-end-of-my-powerlevel10k-prompt-mean)

## Additional Resources

_Source: [Make Your Terminal Look Cooler (OMZ + P10k + Starship)](https://www.youtube.com/watch?v=WXiNkZVmkD4)_
