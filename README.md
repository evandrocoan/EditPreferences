=== Description ===

Some commands for Sublime Text 3 (NOT 2!) to list shortcut keys / preferences
etc in the QuickPanel and navigate to edit location on selection.


## Installation

### By Package Control

1. Download & Install `Sublime Text 3` (https://www.sublimetext.com/3)
1. Go to the menu `Tools -> Install Package Control`, then,
   wait few seconds until the `Package Control` installation finishes
1. Go to the menu `Preferences -> Package Control`
1. Type `Package Control Add Channel` on the opened quick panel and press <kbd>Enter</kbd>
1. Then, input the following address and press <kbd>Enter</kbd>
   ```
   https://raw.githubusercontent.com/evandrocoan/StudioChannel/master/channel.json
   ```
1. Now, go again to the menu `Preferences -> Package Control`
1. This time type `Package Control Install Package` on the opened quick panel and press <kbd>Enter</kbd>
1. Then, search for `EditPreferences` and press <kbd>Enter</kbd>

See also:
1. [ITE - Integrated Toolset Environment](https://github.com/evandrocoan/ITE)
1. [Package control docs](https://packagecontrol.io/docs/usage) for details.


=== 2000 Words ===

{{http://ndudfield.com/zencoding/old/editprefs-settings.gif}}

{{http://ndudfield.com/zencoding/old/editprefs.gif}}

=== How to insert a binding repr in the Quick Panel ===

Copy from the Default.sublime-keymap.template the last line that contains a
multitude of bindings with `insert_binding_repr` and place it in your User
keymap.


So how would you insert alt+q? You can think of it like this:

    * PRESS `alt` and hold it down
    * PRESS `=` while thinking PLUS then lift all fingers
    * PRESS `q`

Note that on a standard US keyboard `=` is on the same key as `+` (plus)  You
can't bind to just a modifier like alt, so plus seems a resaonable key/mnemonic.

In sublime `{"keys": [...]}` terms previous exmaple would be:

    * PRESS `["alt+="]`
    * PRESS `["q"]`

The following bindings show how it works.
Note the `expecting_binding_repr_mode` key.

```js
    {"args": {"val": "alt"},
     "command": "insert_binding_repr",
     "context": [{"key": "overlay_visible", "operand": true, "operator": "equal"},
                 {"key": "setting.expecting_binding_repr_mode",
                  "operand": false,
                  "operator": "equal"}],
     "keys": ["alt+="]}
```

```js
     {"args": {"val": "q"},
      "command": "insert_binding_repr",
      "context": [{"key": "overlay_visible", "operand": true, "operator": "equal"},
                  {"key": "setting.expecting_binding_repr_mode",
                   "operand": true,
                   "operator": "equal"}],
      "keys": ["q"]}
```

So how would you insert ctrl+alt+q? (In sublime terms)

    * PRESS `ctrl+alt+=`
    * PRESS `q`

=== Help? You can't insert_binding_repr for down|enter|up ? ===

Unfortunately, some bindings don't work as the second key due to the quickpanel
swallowing them:

    * <enter>
    * <up>
    * <down>
    * and others ...

The workaround is to type the first letter of the key you desire, eg:

    * type `e` for <enter> to insert `alt+e` then type `nter`
    * type `u` for <up> to insert `alt+u` then type `p`
    * type `d` for <down>  to insert `alt+d` then type `own`

=== Command Palette ===

```js
[
    { "caption": "Edit Preference: List Settings",         "command": "list_settings"},
    { "caption": "Edit Preference: List Plugins Commands", "command": "list_commands" },
    { "caption": "Edit Preference: List Shortcut Keys",    "command": "list_shortcut_keys"},
    { "caption": "Edit Preference: List Menu Bindings",    "command": "list_menu_bindings"},

    { "caption": "Edit Preference: Theme",
      "command": "edit_package_files",
      "args": {"pref_type": "sublime-theme"}},

    { "caption": "Edit Preference: sublime-completions",
      "command": "edit_package_files",
      "args": {"pref_type": "sublime-completions"}},

    { "caption": "Edit Preference: sublime-build",
      "command": "edit_package_files",
      "args": {"pref_type": "sublime-build"}},

    { "caption": "Edit Preference: sublime-mousemap",
      "command": "edit_package_files",
      "args": {"pref_type": "sublime-mousemap"}},

    { "caption": "Edit Preference: sublime-menu",
      "command": "edit_package_files",
      "args": {"pref_type": "sublime-menu"}},

    { "caption": "Edit Preference: tmTheme|colorscheme",
      "command": "edit_package_files",
      "args": {"pref_type": ".*\\.(tmTheme|stTheme)$"}},

    { "caption": "Edit Preference: tmLanguage|syntax|grammar",
      "command": "edit_package_files",
      "args": {"pref_type": ".*\\.((tm|st)Language)$"}},

    { "caption": "Edit Preference: sublime-commands",
      "command": "edit_package_files",
      "args": {"pref_type": "sublime-commands"}}
]
```

=== TODO ===

Set cyclic tab key for auto complete

