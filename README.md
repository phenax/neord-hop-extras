# neorg-hop-extras
Neorg plugin to extend the functionality of links


## Install

#### For [packer](https://github.com/wbthomason/packer.nvim) users -
```lua
  use {
    'nvim-neorg/neorg',
    -- ...
    requires = {
      -- ...
      {'phenax/neorg-hop-extras'},
    }
  }
```


#### Basic config
```lua
require('neorg').setup {
  load = {
    -- ...
    ['external.hop-extras'] = {},
    ['core.keybinds'] = {
      config = {
        hook = neorg_keybindings,
      }
    },
  },
}

function neorg_keybindings(keybinds)
  -- Use `external.hop-extras.hop-link` instead of `core.esupports.hop.hop-link`
  keybinds.map_event_to_mode("norg", {
    n = {
      { "<CR>", "external.hop-extras.hop-link", opts = { desc = "Follow link" } },
    }
  }, { silent = true, noremap = true })
end
```


## Usage

#### Commands as links
Run an arbitrary vim command when a link is activated

```neorg
- Increment counter {+norm! t]}[Count: 19] - increments the count every time the link is activated
- View yesterday's journal {+Neorg journal yesterday}[Yesterday] - Opens yesterday's journal
- Insert timelog into routine {+Neorg timelog insert routine}[Log routine] (requires [phenax/neorg-timelog](https://github.com/phenax/neorg-timelog))
```

#### Aliases for links
Use aliases for links

```neorg
- Github url - {&gh phenax/neorg-timelog}
- Npm package link - {&npm react}
- Rust package link - {&crates serde}
- Dart package link - {&pub serde}
- Twitter user @Neovim - {&tw Neovim} (Custom alias defined below)
```

To define the custom alias, use -
```lua
require('neorg').setup {
  load = {
    -- ...
    ['external.hop-extras'] = {
      config = {
        aliases = {
          tw = 'https://twitter.com/{}'
        },
      },
    },
  },
}
```

#### Ask for confirmation before opening link
Ask for confirmation (uses `vim.fn.confirm`) before activating a link

```neorg
  - Asks for confirmation before opening external link - {! https://example.com}
  - Confirm before opening alias - {! &npm react}
  - Confirm before running command {! +norm! t]}[16]
```


