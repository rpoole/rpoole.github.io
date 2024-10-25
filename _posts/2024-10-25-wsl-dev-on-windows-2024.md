I recently got a new Windows PC and decided to set it up for programming work.
I prefer the developer experience on Linux/Mac (the former more than the
latter), but really don't like switching computers or maintaining multiple
boots.

I've used WSL in the past, and it's a perfect compromise.

I periodically redo my setup from scratch. I do it to give all the tools I use
a refresher. It's a natural way of exploring what new tools are out there and
weighing them against what I currently use. This article will cover the October 2024 edition of that venture.


### WSL

This was even easier than I remember. A quick google landed me on the [WSL
install page](https://learn.microsoft.com/en-us/windows/wsl/install){:target="_blank"}. All it
took was a quick:
{% highlight powershell %}
wsl --install
{% endhighlight %}

Don't skip [the best practices page](https://learn.microsoft.com/en-us/windows/wsl/setup/environment){:target="_blank"}! You'll probably
want to do some of the suggestions and there's some good tips as well.

### Terminal Emulator

I generally don't use my terminal for much aside from input/output.
I prefer tools I can take with me and that's not often the case with terminal
emulators.

The two things I'm looking for in a terminal are:
1. **Performant**. I'm only using this thing for input/output, so any extra
   features that hinder performance I gain nothing from.
2. **Well supported/Easy to use**. I don't consider tinkering with my terminal a good use
   of my time (please let me know if I'm wrong). After I set my initial colors,
   font, and disable that annoying bell, I don't want to touch it again.

I considered 3 options:

#### [Windows Terminal](https://learn.microsoft.com/en-us/windows/terminal/install){:target="_blank"}

I've always used this terminal with WSL in the past, primarily because it was
the best supported. I started using WSL early on so there weren't many other
options. It was a bit slow at times, but it otherwise did what I wanted. This
is my fallback if the other 2 don't work out.

#### [Alacritty](https://alacritty.org/){:target="_blank"}

After doing some research, I decided against Alacritty. Portability is cool,
but given my limited dependence on terminal features it wasn't a big draw for
me. And a big deterrent was that windows appeared to be a second class citizen.
That's a big strike against **well supported**.

#### [WezTerm](https://wezfurlong.org/wezterm/index.html){:target="_blank"}

I'd never heard of WezTerm before, though apparently it's been around since 2019. It claims to be fast and that appears to be true. The support for it
seemed decent as I was able to cobble together my desired config file pretty
easily. From what I could tell Windows support is good.

One other thing that really piqued my interest was it's ability to replace
tmux. I primarily use tmux for the window/session management (I'm not often
remoting in to servers doing local dev), so if I could drop tmux that would be
a nice simplification to make. I spent a few hours following some guides trying
to get an equivalent setup working, but unfortunately it fell short. It was
close! The dealbreaker was lack of persistent sessions. I found some
attempts at it by others, and while it looks like it might be possible, it was
more work than I wanted to do. When it came to regular window/session usage
it worked great! I was able to get to a nearly 1:1 setup with tmux.

Tmux replacement was a bonus, and WezTerm was enjoyable enough that I've
decided to give it a shot. Worst case I'm back on windows terminal.

- [Config file link](https://github.com/rpoole/dotfiles/blob/master/.wezterm.lua) (tmux parity
config is there commented out){:target="_blank"}

### Command Line Tools

I prefer to spend the majority of my time in the command line. I don't enjoy
using a mouse, and CLI tools tend to be good time investments.

For all the tools below, installing these in WSL was very simple. The only WSL
specific hiccup was getting copy/paste working in NVIM.

#### [ZSH](https://ohmyz.sh/){:target="_blank"}

I should invest more time into learning my shell but haven't. I was a long time
bash user until mac switched to zsh (most work laptops I've had are macs), so
I use zsh now. I'd like to try fish shell one day, but zsh works for now. My
usage of it is pretty entry level.

- [Config file link](https://github.com/rpoole/dotfiles/blob/master/.zshrc){:target="_blank"}

#### [NeoVim](https://neovim.io/){:target="_blank"}

I've been a long time Vim user, and switched to NeoVim awhile ago. It's been
around a long time and I like to believe the [Lindy
Effect](https://en.wikipedia.org/wiki/Lindy_effect){:target="_blank"} is true.

Getting the clipboard working with WSL required a little extra config. I had to
install win32 yank:
1. Download the exe from here `https://github.com/equalsraf/win32yank/releases`
2. `sudo mv win32yank.exe /usr/bin`

then add this snippet to my nvim config:

{% highlight lua %}
-- WSL clipboard
vim.g.clipboard = {
    name = "win32yank-wsl",
    copy = {
        ["+"] = "win32yank.exe -i --crlf",
        ["*"] = "win32yank.exe -i --crlf",
    },
    paste = {
        ["+"] = "win32yank.exe -o --lf",
        ["*"] = "win32yank.exe -o --lf",
    },
    cache_enabled = true,
}
vim.opt.clipboard = "unnamedplus"
{% endhighlight %}

I could probably write a whole article about my nvim config, and maybe I will
one day. For now it's accessible below.
- [Config file link](https://github.com/rpoole/dotfiles/tree/master/.config/nvim){:target="_blank"}

#### [tmux](https://github.com/tmux/tmux/wiki){:target="_blank"}

Since I spend a lot of time in the CLI I need a tool to organize my various
shells and groupings of shells (tmux sessions). I quickly found tmux after I 
started developing and have used it since. As mentioned above, my primary usage
of it is managing various shells, but being comfortable with a tool to keep
remote sessions alive is handy as well.

Missing the combo of `tmux-resurrect` and `tmux-continuum` are what kept me from
replacing tmux with WezTerm.

- [Config file link](https://github.com/rpoole/dotfiles/blob/master/.tmux.conf){:target="_blank"}

### All Done

After I installed all the tools above (as well as some additional accompanying
ones not covered, but are listed in the config files) I was all setup on WSL.
All in all it took me a few hours and was a pretty enjoyable process!
