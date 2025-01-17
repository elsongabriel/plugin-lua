<p align="center">
    🚧 &nbsp;Work in Progress!&nbsp;🚧
</p>

<div align="center">
<img alt="Prettier"
  src="https://raw.githubusercontent.com/prettier/prettier-logo/master/images/prettier-icon-light.png">
<img alt="Lua" height="180" hspace="25" vspace="15"
  src="https://commons.wikimedia.org/wiki/Special:Redirect/file/Lua-logo-nolabel.svg">
</div>

<h2 align="center">Prettier Lua Plugin</h2>

## WORK IN PROGRESS

Please note that this plugin is currently in alpha stage and still under active development. We encourage everyone to try it and give feedback, but we don't recommend it for production use yet.

## Intro

Prettier is an opinionated code formatter. It enforces a consistent style by parsing your code and re-printing it with its own rules that take the maximum line length into account, wrapping code when necessary.

This plugin adds support for the Lua language to Prettier.

### Input

```lua
function deepcopy(orig)
  local orig_type = type(orig)
     local copy

  if orig_type == 'table' then; copy = {}
  for orig_key, orig_value in next, orig, nil do
  copy[deepcopy(orig_key)] = deepcopy(orig_value)
          end
          setmetatable(
            copy,
            deepcopy(
              getmetatable(orig)))
      else
          copy = orig
      end
    return copy
  end
```

### Output

```lua
function deepcopy(orig)
	local orig_type = type(orig)
	local copy

	if orig_type == "table" then
		copy = {}
		for orig_key, orig_value in next, orig, nil do
			copy[deepcopy(orig_key)] = deepcopy(orig_value)
		end
		setmetatable(copy, deepcopy(getmetatable(orig)))
	else
		copy = orig
	end
	return copy
end
```

## Install

yarn:

```bash
yarn add --dev @elsongabriel/prettier @elsongabriel/lua-formatter
```

npm:

```bash
npm install --save-dev @elsongabriel/prettier @elsongabriel/lua-formatter
```

## Use and Testing

If you installed `@elsongabriel/lua-formatter` in your project, you can add those scripts in your `package.json`

```json
"scripts": {
  "prettier": "prettier --plugin=@elsongabriel/lua-formatter --parser=lua",
  "prettier:format": "npm run prettier --write \"**/*.lua\"",
  "prettier:test": "npm run prettier --write path/to/file.lua"
}
```

and then run it via command

```bash
# check and format all files
npm run prettier:format
```

```bash
# check and format passing file
yarn run prettier --write path/to/file.lua
# or
npm run prettier --write path/to/file.lua
```

### Testing our `@elsongabriel/lua-formatter`
Check and format all files before you run in your project
- First copy your lua file to lua-tests folder
- Run command below
```bash
npm run prettier:test
```

## Editor integration

Integration in the prettier plugin for your favorite editor might not be working yet, see the related issues for [VS Code](https://github.com/prettier/prettier-vscode/issues/395), [Atom](https://github.com/prettier/prettier-atom/issues/395) and [Vim](https://github.com/prettier/vim-prettier/issues/119).

For the moment, you can set up prettier to run on save like this:

### Atom

Install [save-autorun](https://atom.io/packages/save-autorun) and create a `.save.cson` file in your project with the following content:

```cson
"**/*.lua": "npm run prettier ${path} --write"
```

### VScode

Install [Run on Save](https://marketplace.visualstudio.com/items?itemName=emeraldwalk.RunOnSave) and add the following section to your settings:

```json
"emeraldwalk.runonsave": {
  "commands": [
    {
      "match": "\\.lua$",
        "cmd": "npm run prettier ${file} --write"
    }
  ]
}
```

### Vim

Adding the following to `.vimrc` will define a custom command `:PrettierLua` that runs the plugin while preserving the cursor position and run it on save.

```vim
" Prettier for Lua
function PrettierLuaCursor()
  let save_pos = getpos(".")
  %! prettier --stdin --parser=lua
  call setpos('.', save_pos)
endfunction
" define custom command
command PrettierLua call PrettierLuaCursor()
" format on save
autocmd BufwritePre *.lua PrettierLua
```

### Sublime Text

Install [JsPrettier](https://packagecontrol.io/packages/JsPrettier) using [Package Control](https://packagecontrol.io/installation) and add the following to your `<project_name>.sublime-project` project-level file:

```
{
  "settings": {
    "js_prettier": {
      "auto_format_on_save": true,
      "custom_file_extensions": ["lua"],
    }
  }
}

```

Alternatively, `"custom_file_extensions": ["lua"]` can be added to the JsPrettier plugin user settings.
