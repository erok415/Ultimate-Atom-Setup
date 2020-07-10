# Ultimate Atom Setup

Checkout this great write up by Elad Ossadon on the Ulitmate Atom Editor Setup. [Source link](https://medium.com/productivity-freak/my-atom-editor-setup-for-js-react-9726cd69ad20)

To install everything run the following snippet in your favorite terminal app. I use [iTerm2](https://www.iterm2.com/) (I removed one-dark-ui referenced from the article since Atom includes this as a default in the latest release): 

```
apm install atom-beautify prettier-atom atom-spotify2 atom-transpose case-keep-replace change-case copy-path 
duplicate-line-or-selection editorconfig file-icons git-plus highlight-selected local-history project-manager 
related set-syntax sort-lines sublime-style-column-selection tab-foldername-index sync-settings toggle-quotes 
atom-wrap-in-tag atom-ternjs autoclose-html autocomplete-modules color-picker docblockr emmet emmet-jsx-css-modules 
es6-javascript js-hyperclick hyperclick pigments linter-eslint tree-view-copy-relative-path lodash-snippets 
language-babel react-es7-snippets atom-jest-snippets dracula-theme
```

Here's some additional goodies.
```
apm install git-time-machine minimap
```
# Now, let's get that CLI set up...

Working with a plain vanilla CLI terminal setup on your Mac or Ubuntu setup get's boring fast. You probably want to know what directory you're on, you may not what to see who you're logged in as, and you most likely want to see the git branch you're on too. To achieve all of this, I love using iTerm2. It's the ultimate Terminal setup and offers a lot of customization.

[iTerms2](https://www.iterm2.com/) is a fantastic CLI. So let's get started.

## 1. First, let's install iTerm2 with brew.

```
brew cask install iterm2
```
If you don’t have installed homebrew (you should… ;)), [download](http://www.iterm2.com/downloads.html) and install iTerm2 (it has better color fidelity than the built in Terminal, so your themes will look better).

## 2. Install a patched font
The patched font is the font used by iTerm2 to display characters, and you’ll need a special one for special characters like arrows and git icons.

**Download and install the font**
- [Meslo](https://github.com/powerline/fonts/blob/master/Meslo%20Slashed/Meslo%20LG%20M%20Regular%20for%20Powerline.ttf) (recommanded, ie the one in the screenshot). Click “view raw” to download the font.
- [Source Code Pro](https://github.com/powerline/fonts/blob/master/SourceCodePro/Source%20Code%20Pro%20for%20Powerline.otf) has better alignment for the glyphs @14px.
- [Others powerline fonts](https://github.com/powerline/fonts)
Open the downloaded font and press “Install Font” on your computer.
**Add the font in iTerm2**
(font size of 12pt is our personal preference)
`iTerm2 → Preferences → Profiles → Text → Change Font`

## 3. Install Zsh and Oh my Zsh
Zsh is a shell that provides many features, like better files and folders navigation. To install it :
```
brew install zsh zsh-completions
```
Oh my Zsh is a Zsh configuration framework, you can read more here: github.com/robbyrussell/oh-my-zsh.
To install it :
```
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
💡In the next steps you’ll need to edit the ~/.zshrc configuration file which is run when the terminal starts. At any time you can compare it with [Clovis .zshrc configuration file](https://github.com/Clovis-team/clovis-open-code-extracts/blob/master/utils/clovis-zshrc) 🎁

## 4. Add Powerlevel9k Zsh Theme
The Powerlevel9k zsh theme adds many other features like a right promp with infos such as exit codes and timestamps. To install it run :
```
git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
```
Then edit ~/.zshrc configuration file and set
```
ZSH_THEME="powerlevel9k/powerlevel9k"
```
Powerlevel9k offers a whole lot more, best is to follow the next steps or [check out these user made configs](https://github.com/bhilburn/powerlevel9k/wiki/Show-Off-Your-Config).

## 5. Final tweaking
- shorter prompt
- enable text editor navigation
- auto suggestions
- syntax highlighting
- new line after each prompt
- change color of warning git status
- change Iterm2 tabs color

**Shorter prompt**
Here you can remove the user@hostname and unnecessary informations + put the command line on a second prompt line :

You can choose your prompt elements and make them as on the screenshots. Just add these lines to your ~/.zshrcconfiguration file :
```
POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(dir rbenv vcs)
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status root_indicator background_jobs history time)
```
Moreover to make the two lines prompt you have to add this:
<pre>
POWERLEVEL9K_PROMPT_ON_NEWLINE=true
</pre>
💄✨ and to make it beautifull with the $ character add these other lines:
<pre>
# Add a space in the first prompt
POWERLEVEL9K_MULTILINE_FIRST_PROMPT_PREFIX="%f"
# Visual customisation of the second prompt line
local user_symbol="$"
if [[ $(print -P "%#") =~ "#" ]]; then
    user_symbol = "#"
fi
POWERLEVEL9K_MULTILINE_LAST_PROMPT_PREFIX="%{%B%F{black}%K{yellow}%} $user_symbol%{%b%f%k%F{yellow}%} %{%f%}"
</pre>
You can read more about POWERLEVEL9K prompts options [here](https://github.com/bhilburn/powerlevel9k#customizing-prompt-segments), and deeper customizations here: code.tutsplus.com/tutorials/how-to-customize-your-command-prompt — net-24083

**Enable text editor navigation**
Vertical cursor
<pre>
iTerm2 → Preferences → Profiles → Text
→ Cursor : ✓ Vertical Bar 
→ Blinking cursor : ✓ ON
</pre>
**Text navigation with keyboard**
Moreover, by default, word jumps (option + → or ←) and word deletions (option + backspace) do not work on iTerm2. To enable them, go to :
```
iTerm → Preferences → Profiles → Keys → Load Preset… → Natural Text Editing
```
Restart iTerm2 for all changes to take effect.

**Auto suggestions (for Oh My Zsh)**
This plugin suggests the commands you used in your terminal history. You just have to type → to fill it entirely!
```
$ git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
Note: $ZSH_CUSTOM/plugins path is by default ~/.oh-my-zsh/custom/plugins
```
Add the plugin to the list of plugins in ~/.zshrcconfiguration file :
```
plugins=(
    …
    zsh-autosuggestions
)
```
Start a new terminal session.

More details here : github.com/tarruda/zsh-autosuggestions#oh-my-zsh

Source: For more tips, visit https://medium.com/@Clovis_app/configuration-of-a-beautiful-efficient-terminal-and-prompt-on-osx-in-7-minutes-827c29391961
