---
title: "How to Write a Neovim Plugin"
date: 2023-07-16T20:06:02-03:00
draft: true
---

1) Create a github project with the name of the project with ".nvim" at the end
    * Example: stackmap.nvim
2) If you wanna test it locally using folke/lazy.nvim you gotta add another bracket like:
```lua
    {
      dir = 'path/to/your/local/plugin_name.nvim',
      lazy = true
    }
```
3) By default everything that is inside the /plugin inside your plugin folder will be
automatically executed and those that live inside the /lua plugin gotta be "required".
What is meant by required is this `:lua require("plugin_name")`

4) If you wanna require any other file besides the one called init.lua inside a folder,
you gotta put the entire path. For example, let's say you have an utils.lua inside
`plugin_name/lua/plugin_name/utils.lua`, for you to lead that utils you gotta run
`:lua require("plugin_name.utils")`

5) For you to access functions inside lua that you call inside command mode, inside the script
in lua that you are writting, you gotta call `vim.api.name_of_function`



## Contents

- [Features](#features)
  - [Light and Dark mode](#light-and-dark-mode)
