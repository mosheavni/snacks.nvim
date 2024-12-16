# 🍿 styles

Plugins provide window styles that can be customized
with the `opts.styles` option of `snacks.nvim`.

<!-- docgen -->

## 📦 Setup

```lua
-- lazy.nvim
{
  "folke/snacks.nvim",
  ---@type snacks.Config
  opts = {
    ---@type table<string, snacks.win.Config>
    styles = {
      -- your styles configuration comes here
      -- or leave it empty to use the default settings
      -- refer to the configuration section below
    }
  }
}
```

## 🎨 Styles

These are the default styles that Snacks provides.
You can customize them by adding your own styles to `opts.styles`.


### `blame_line`

```lua
{
  width = 0.6,
  height = 0.6,
  border = "rounded",
  title = " Git Blame ",
  title_pos = "center",
  ft = "git",
}
```

### `dashboard`

The default style for the dashboard.
When opening the dashboard during startup, only the `bo` and `wo` options are used.
The other options are used with `:lua Snacks.dashboard()`

```lua
{
  zindex = 10,
  height = 0,
  width = 0,
  bo = {
    bufhidden = "wipe",
    buftype = "nofile",
    buflisted = false,
    filetype = "snacks_dashboard",
    swapfile = false,
    undofile = false,
  },
  wo = {
    colorcolumn = "",
    cursorcolumn = false,
    cursorline = false,
    foldmethod = "manual",
    list = false,
    number = false,
    relativenumber = false,
    sidescrolloff = 0,
    signcolumn = "no",
    spell = false,
    statuscolumn = "",
    statusline = "",
    winbar = "",
    winhighlight = "Normal:SnacksDashboardNormal,NormalFloat:SnacksDashboardNormal",
    wrap = false,
  },
}
```

### `float`

```lua
{
  position = "float",
  backdrop = 60,
  height = 0.9,
  width = 0.9,
  zindex = 50,
}
```

### `input`

```lua
{
  backdrop = false,
  position = "float",
  border = "rounded",
  title_pos = "center",
  height = 1,
  width = 60,
  relative = "editor",
  noautocmd = true,
  row = 2,
  -- relative = "cursor",
  -- row = -3,
  -- col = 0,
  wo = {
    winhighlight = "NormalFloat:SnacksInputNormal,FloatBorder:SnacksInputBorder,FloatTitle:SnacksInputTitle",
    cursorline = false,
  },
  bo = { filetype = "snacks_input" },
  --- buffer local variables
  b = {
    completion = false, -- disable blink completions in input
  },
  keys = {
    i_esc = { "<esc>", { "cmp_close", "cancel" }, mode = "i" },
    -- i_esc = { "<esc>", "stopinsert", mode = "i" },
    i_cr = { "<cr>", { "cmp_accept", "confirm" }, mode = "i" },
    i_tab = { "<tab>", { "cmp_select_next", "cmp" }, mode = "i" },
    q = "cancel",
  },
}
```

### `lazygit`

```lua
{}
```

### `minimal`

```lua
{
  wo = {
    cursorcolumn = false,
    cursorline = false,
    cursorlineopt = "both",
    fillchars = "eob: ,lastline:…",
    list = false,
    listchars = "extends:…,tab:  ",
    number = false,
    relativenumber = false,
    signcolumn = "no",
    spell = false,
    winbar = "",
    statuscolumn = "",
    wrap = false,
    sidescrolloff = 0,
  },
}
```

### `notification`

```lua
{
  border = "rounded",
  zindex = 100,
  ft = "markdown",
  wo = {
    winblend = 5,
    wrap = false,
    conceallevel = 2,
    colorcolumn = "",
  },
  bo = { filetype = "snacks_notif" },
}
```

### `notification_history`

```lua
{
  border = "rounded",
  zindex = 100,
  width = 0.6,
  height = 0.6,
  minimal = false,
  title = " Notification History ",
  title_pos = "center",
  ft = "markdown",
  bo = { filetype = "snacks_notif_history", modifiable = false },
  wo = { winhighlight = "Normal:SnacksNotifierHistory" },
  keys = { q = "close" },
}
```

### `scratch`

```lua
{
  width = 100,
  height = 30,
  bo = { buftype = "", buflisted = false, bufhidden = "hide", swapfile = false },
  minimal = false,
  noautocmd = false,
  -- position = "right",
  zindex = 20,
  wo = { winhighlight = "NormalFloat:Normal" },
  border = "rounded",
  title_pos = "center",
  footer_pos = "center",
}
```

### `split`

```lua
{
  position = "bottom",
  height = 0.4,
  width = 0.4,
}
```

### `terminal`

```lua
{
  bo = {
    filetype = "snacks_terminal",
  },
  wo = {},
  keys = {
    q = "hide",
    gf = function(self)
      local f = vim.fn.findfile(vim.fn.expand("<cfile>"), "**")
      if f == "" then
        Snacks.notify.warn("No file under cursor")
      else
        self:hide()
        vim.schedule(function()
          vim.cmd("e " .. f)
        end)
      end
    end,
    term_normal = {
      "<esc>",
      function(self)
        self.esc_timer = self.esc_timer or (vim.uv or vim.loop).new_timer()
        if self.esc_timer:is_active() then
          self.esc_timer:stop()
          vim.cmd("stopinsert")
        else
          self.esc_timer:start(200, 0, function() end)
          return "<esc>"
        end
      end,
      mode = "t",
      expr = true,
      desc = "Double escape to normal mode",
    },
  },
}
```

### `zen`

```lua
{
  enter = true,
  fixbuf = false,
  minimal = false,
  width = 120,
  height = 0,
  backdrop = { transparent = true, blend = 40 },
  keys = { q = false },
  wo = {
    winhighlight = "NormalFloat:Normal",
  },
}
```

### `zoom_indicator`

fullscreen indicator
only shown when the window is maximized

```lua
{
  text = "▍ zoom  󰊓  ",
  minimal = true,
  enter = false,
  focusable = false,
  height = 1,
  row = 0,
  col = -1,
  backdrop = false,
}
```