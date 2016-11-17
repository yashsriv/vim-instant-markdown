vim-instant-pandoc
====================
Want to instantly preview pandoc markdown files, but don't want to leave your favorite editor, or have to do it in some crappy browser textarea?
**vim-instant-pandoc** is a plugin which launches a browser window showing the compiled html5 in real-time, and closes once you close the file in vim.

This was originally thought of by @[suan](https://github.com/suan). I can't thank him enough for the work he has done. I have merely changed the
executable in my fork. Even this readme has just been modified for specific things while others remain nearly the same.

Installation
------------
You first need to have node.js with npm installed. Then:

- `[sudo] npm -g install instant-pandoc-d`
- If you're on Linux, ensure the following packages are installed:
  - `xdg-utils`
  - `curl`
  - `nodejs-legacy` (for Debian-based systems)
- If you're on Windows, you will need into install [cURL][curl] and put it on your `%PATH%`.
- Install `vim-pandoc/vim-pandoc` plugin. See [FAQ](#faq)
- Copy the `after/ftplugin/markdown/instant-pandoc.vim` file from this repo into your `~/.vim/after/ftplugin/markdown/` (creating directories as necessary), or follow your vim package manager's instructions.
- Ensure you have the line `filetype plugin on` in your `.vimrc`
- Open a pandoc markdown file in vim and enjoy!

Configuration
-------------

### g:instant_pandoc_port
By default, port 8090 is used for the server.
To change the port, edit your .vimrc and add

```
let g:instant_pandoc_port = 8080
```

### g:instant_pandoc_slow

By default, vim-instant-pandoc will update the display in realtime.  If that taxes your system too much, you can specify

```
let g:instant_pandoc_slow = 1
```

before loading the plugin (for example place that in your `~/.vimrc`). This will cause vim-instant-pandoc to only refresh on the following events:

- No keys have been pressed for a while
- A while after you leave insert mode
- You save the file being edited

### g:instant_pandoc_autostart
By default, vim-instant-pandoc will automatically launch the preview window when you open a markdown file. If you want to manually control this behavior, you can specify

```
let g:instant_pandoc_autostart = 0
```

in your .vimrc. You can then manually trigger preview via the command `:InstantPandocPreview`. This command is only available inside markdown buffers and when the autostart option is turned off.

### g:instant_pandoc_open_to_the_world
By default, the server only listens on localhost. To make the server available to others in your network, edit your .vimrc and add

```
let g:instant_pandoc_open_to_the_world = 1
```

Only use this setting on trusted networks!

### g:instant_pandoc_allow_unsafe_content
By default, scripts are blocked. To allow scripts to run, edit your .vimrc and add

```
let g:instant_pandoc_allow_unsafe_content = 1
```

### g:instant_pandoc_allow_external_content
By default, external resources such as images, stylesheets, frames and plugins are allowed.
To block such content, edit your .vimrc and add

```
let g:instant_pandoc_allow_external_content = 0
```

Supported Platforms
-------------------
OSX, Unix/Linuxes*, and Windows**.

<sub>*: One annoyance in Linux is that there's no way to reliably open a browser page in the background, so you'll likely have to manually refocus your vim session everytime you open a Markdown file. If you have ideas on how to address this I'd love to know!</sub>

<sub>**: In Windows, there's no easy way to execute commands asynchronously without popping up a cmd.exe window. Thus, if you run this plugin without `g:instant_pandoc_slow`, you might experience performance issues.</sub>

FAQ
---
> It's not working!

- Make sure `instant-pandoc-d` was installed as a global module (e.g. using `npm -g install`)
- If you're on OSX and are using zsh, try to add `set shell=bash\ -i` in your `.vimrc` to set interactive bash as the default vim shell. (See [this issue](http://github.com/suan/vim-instant-markdown/issues/41))

> Why don't my `<bla>.md` files trigger this plugin?

By default, vim doesn't recognise the `pandoc` filetype at all. To add support for it I will recommend:

* [vim-pandoc][vim-pandoc]: Basic `filetype` detection support
* [vim-pandoc-syntax][vim-pandoc-syntax]: Basic syntax support

etc.
---
If you're curious, the code for the mini-server component for this plugin can be found at [https://github.com/yashsriv/instant-pandoc-d](https://github.com/yashsriv/instant-pandoc-d). A plugin can easily be written for any editor to interface with the server to get the same functionality found here.

[vim-pandoc]: https://github.com/vim-pandoc/vim-pandoc
[vim-pandoc-syntax]: https://github.com/vim-pandoc/vim-pandoc-syntax
[curl]: http://curl.haxx.se/download.html
