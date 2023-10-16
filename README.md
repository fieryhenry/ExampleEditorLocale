# Example Locale

This is an example repo for an external locale for my [Save
Editor](https://github.com/fieryhenry/BCSFE-Python).

If you want to make your own locale for the editor, you can fork this repo and
edit the `locale.json` file and files in the `files` folder. You can also
translate the `README.md` file if you want.

If you need help, or want any extra features, you can join the [Discord
server](https://discord.gg/DvmMgvn5ZB) and ask in the `#tool-dev` channel, or
make suggestions in the `#suggestions` channel.

## How to make a locale

1. Fork this repo
2. Edit the `locale.json` file
3. Edit the .properties files in the `files` folder (the names of the
   files and the folders they are contained in don't matter)
4. Install [git](https://git-scm.com/downloads)
5. In the editor, go to `Edit config` -> `Language` -> `Add Locale`
6. Enter the URL of your forked repo (with the `.git` at the end)
7. Restart the editor to see the changes

The locale will be cloned into the `external_locales` folder in `bcsfe` in your
documents folder. The folder name will be `ext-<author>-<short_name>` so that
collisions with other locales are avoided.

## Locale.json file

The `locale.json` file contains some metadata about the locale. Here are what
the different fields mean:

- `short_name`: The short code for the locale (e.g. `en` for English).
- `name`: The name of the locale (e.g. `English`). This is what will be shown in
  the editor to the user.
- `author`: The name of the author of the locale.
- `version`: The version of the locale. This is used to check for updates to the
  locale. Every time you want to release an update to the locale, you should
    increase this. It can be any string, but it is recommended to use
    [semantic versioning](https://semver.org/).
- `description`: A description of the locale. This is shown in the editor to the
  user.

## Files folder

The `files` folder contains the actual translations for the text in the editor.
The files have the `.properties` extension, but they are just text files. The
names of the files don't matter, nor do the folder names, but it is recommended
to use the same name as the English file that you are translating.

## Format of the .properties files

The format is loosely based on the Java `.properties` file format. Each line is a
key-value pair, where the key is the English string and the value is the
translation. The key and value are separated by an equals sign (`=`). For
example:

```properties
save_load_option=Select an option to load the save file
```

If you duplicate a key, the editor will throw an error.

Any strings that are not overwritten in your locale will be taken from the
   default locale (English)

### Newlines

Newlines are represented by `\n`. For example:

```properties
cant_detect_cc=Failed to detect country code from save file. \nPlease enter your country code manually
```

### Tabs

Tabs are represented by `\t`. For example:

```properties
failed_to_load_save=Failed to load save file\tReason: ...
```

### Backslashes

Backslashes are represented by `\`, and can be used to escape other characters.

```properties
WARNING: Editing your inquiry code can result in your account being unplayable.\\nUse at your own risk.
```

The above text will be displayed as:

```text
WARNING: Editing your inquiry code can result in your account being unplayable.\nUse at your own risk.
```

This is not a very good example, but it shows how to escape a newline.

### Comments

Comments are lines that start with a `#`. For example:

```properties
# This is a comment
```

The editor will ignore these lines.

### Blank lines

Blank lines are ignored by the editor.

### Multiline strings

If you don't want to use the `\n` every time you want a newline, you can use
multiline strings. To start a multiline string, leave the value empty and put a
`>` at the start of every line. For example:

```properties
upload_result=
>Transfer Code: {transfer_code}</>
>Confirmation Code: <@s>{confirmation_code}</>
```

This is mainly used in the en locale for really long strings, but you can use it
anywhere you want.

### Variables

You can use variables in the strings. To use a variable, put the name of the
variable in curly brackets (`{}`). For example:

```properties
selected_skill={name} is selected
```

If the editor passes the variable `name` with the value `Worker Cat`, the string
will be displayed as:

```text
Worker Cat is selected
```

### Embedding other strings

You can embed other strings in a string. To do this, put the name of the string
in double curly brackets (`{{}}`). For example:

```properties
do_you_want_to_continue=Do you want to continue? (y/n):

password_refresh_token_warning=WARNING: Editing your password refresh token can result in your account being unplayable. Use at your own risk.\n{{do_you_want_to_continue}}
```

This will be displayed as:

```text
WARNING: Editing your password refresh token can result in your account being unplayable. Use at your own risk.
Do you want to continue? (y/n):
```

This optional and is purely for convenience and to avoid having to repeat
strings. You can always just copy and paste the string inside the double curly
brackets instead.

### Colors

You can use colors in the strings. To do this, use angle brackets (`<>`) before
the string and then after the string, stop the color with `</>`. There are many
different things you can put in the angle brackets.

#### Hex colors

You can use hex colors in the strings. To do this, put the hex color code in the
angle brackets with a `#` at the start. For example:

```properties
edit_orbs_help=
...
>    <#00FFFF>aku</> - selects <#00FFFF>all aku</> orbs
...
```

I don't recommend using hex colors as they don't take into account the user's
theme.

#### Color names

You can use color names in the strings. To do this, put the color name in the
angle brackets. For example:

```properties
edit_orbs_help=
...
>    <c>aku</> - selects <c>all aku</> orbs
...
```

Here is a list of all the color names you can use:

- `w`: White
- `bl`: Black
- `r`: Red
- `g`: Green
- `b`: Blue
- `y`: Yellow
- `m`: Magenta
- `c`: Cyan
- `dy`: Dark Yellow
- `dg`: Dark Grey
- `db`: Dark Blue
- `dc`: Dark Cyan
- `dm`: Dark Magenta
- `dr`: Dark Red
- `dgn`: Dark Green
- `lg`: Light Grey
- `o`: Orange

Again, I don't recommend using color names as they don't take into account the
user's theme. The only time when these should be used is if the specific color
actually matters, e.g if you want to color the word `red` red, or `aku` cyan.

#### Theme colors

The editor has a theme system, and you can use the theme colors in the strings.
To do this, put the theme color name in the angle brackets with a `@` at the
start. For example:

```properties
no_cc_error=<@e>No game versions found</>
```

Here is a list of all the theme colors you can use:

- `e`: Error
- `w`: Warning
- `su`: Success
- `p`: Primary
- `s`: Secondary
- `t`: Tertiary
- `q`: Quaternary

Details about what each color is used for can be found [here](https://github.com/fieryhenry/ExampleEditorTheme#themejson-file)

Please use these colors instead of hex colors or color names as they take into
account the user's theme.

### Conditional strings

You can change the string depending on the value of a variable.
The format is very complicated to avoid conflicts with the other formats:

```properties
playtime_str=<@t>{hours}</> $(hours: !=1($hours)$, hour)/$
```

The `$(...)/$` is what you wrap the conditional in.

The first `hours:` is the name of the variable

You can separate different conditions with (`$,`).

The first condition `!=1($hours)` can be split into logic and word.

The logic is `!=1` and the word is `hours`. `($` is used to separate the logic
from the word.

`!=1` means that if the variable `hours` is not equal to 1, then the string
`hours` will be used.

Because `hour` is the last condition, if the first condition is not met, then
the string `hour` will be used.

The following is a list of all the logic you can use:

- `==`: Equal to
- `!=`: Not equal to
- `>`: Greater than
- `>=`: Greater than or equal to
- `<`: Less than
- `<=`: Less than or equal to

If the variable `hours` is equal to 1, the example above will display as:

```text
1 hour
```

Otherwise, it will display as:

```text
2 hours
```

### Aliases

For some strings (only really feature options), you can specify different
versions of the same string. For example:

```properties
normal_tickets=Normal Tickets|Basic Tickets|Silver Tickets
```

The first string is displayed to the user, and the other strings will match if
the user types them in. For example, if the user types `Basic Tickets`, it will
match and run the command for `normal_tickets`.
