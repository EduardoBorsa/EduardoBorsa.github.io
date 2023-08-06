---
title: "Neovim Format on Save - No Plugin"
date: 2023-07-15T13:27:57-03:00
---

Now that null-ls is no longer going to be maintained, I was wondering how to get the
same behavior, but without null-ls.

So my end goal is this:
    
    I want to execute format on a specific file whenever I save that file.
    Specifically I want to run the elixir formatter whenever I save an *.ex
    or *.exs file

And the solution is:

```lua
vim.api.nvim_create_autocmd("BufWritePre", {
  group = vim.api.nvim_create_augroup("FormatBeforeSaveElixirFiles", {clear = true}),
  pattern = {"*.ex", "*.exs"},
  callback = function()
    local file_name = vim.api.nvim_buf_get_name(0)

    vim.fn.jobstart({"mix", "format", file_name}, {
      stdout_buffered = true
    })

    vim.cmd(":e!")
  end
})

```

In order to use the snippet of code above you can:

## Option 1

Just create any *.lua file, add the code to it and the run `:source %`, then on the save
neovim session open and elixir file and see if the code is executed.

## Option 2

Add the snippet of code inside a lua file inside your neovim config folder and inside the /after/plugin/
folder. For example: `~/.config/nvim/after/plugin/format_elixir_files_before_save.lua`

Thank you for reading!
