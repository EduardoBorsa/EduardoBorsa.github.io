---
title: "Vim Tips and Tricks"
date: 2023-07-16T20:55:28-03:00
draft: true
---

## Contents

- [How to Check a Normal Mode Mapping?](#how-to-check-a-normal-mode-mapping)
- [When to Use pairs/ipairs for Iterating a Table in Lua?](#when-to-use-pairsipairs-for-iterating-in-lua)
- [What are the Only Two Values That are False in Lua?](#what-are-the-only-two-values-that-are-false-in-lua)
- [How to Write Tests](#how-to-write-tests)

## How to Check a Normal Mode Mapping?
Just type `:nmap PROBLABLE_MAPPING` ~> it will show if there is a mapping associated.
&nbsp;&nbsp;&nbsp;&nbsp;Example:
* `:nmap <leader>tt` ~> This should show the Test this function.

## When to Use pairs/ipairs for Iterating a Table in Lua?
* pairs:
  - iterates over EVERY key in a table
  - order not guaranteed
* ipairs
  - iteratres over ONLY numeric keys in a table
  - order IS guaranteed

## What are the only two values that are false in lua?
Nil and false are the only things that are false in Lua

## How to write tests:
Create a folder called tests in the root folder of you neovim plugin.
inside it create a file that ends with `_spec.lua` and follow the general structure:
```lua
describe("stackmap", function()
  before_each(function()
    -- clean up functions, 
    -- remember that the tests share the same neovim instance
  end)

  it("Test name", function()
    -- test body
    -- assert.are.same({}, {})
  end)
```

## How Does Autocmds work?
it hooks on Events, type :help events to learn more

to list the auto commands for an event run `:au EVENT`, for example: `:au BufEnter`

and it will run everytime you source the file

to clear the autocmd just write :au! BufEnter

the callback inside autocommand when passed as a string will try to call a vimscript function like 'my#plugin#func'

the expand() works as if 

## How Does Autogroups work?
They serve to wrap autocmds, where the default option is {clear = false}

