# Exec

The `exec` command allows you to run short pieces of code within the maze application scope. Code can be specified in the following three ways:

1. _Inline mode:_ inline code specified in the command line as a string argument. `maze exec User.first`
2. _Editor mode:_ a terminal-based code editor is opened and the resulting code is executed once you save and exit. `maze exec`
3. _File mode:_ Code within an existing .cr file is copied to a tmp file for editing and run once editor is closed. `maze exec scripts/stuff.cr`

## Usage

Here is a list of the commands available:

```text
maze exec [OPTIONS] [CODE | FILE_PATH]

Arguments:
  FILE_PATH  Path to a .cr file to run in the application scope (file mode)
  CODE       String containing valid crystal code to run in the application scope (inline mode)

  Note: specifying no argument activates editor mode

Options:
  -e, --editor       Prefered Editor: [vim, nano, pico, etc] (default: vim)
  -b, --back [n]     Load the nth previous script (only valid in editor mode)
```

## Inline Mode

The `exec` command in inline mode allows you to execute a line of code \(or several with semicolons\) with your application code and environment loaded.

Inline mode can be helpful in executing one-liners on a remote production machine, or to quickly execute some code locally.

### Examples:

```text
# Wrapping command in single quotes
$ maze exec 'User.find_by(:email, "test@example.com")'
# Escaping quotes
$ maze exec "User.find_by(:email, \"test@example.com\")"
# Multiple lines of code (using semi-colons)
$ maze exec 'u = User.find(1); u.email if u;'
```

### Full Example:

In this example, an article was accidentally archived, and you want to recover it via command line: 1. Find the article and ensure it exists 1. `maze exec 'Article.find(1)'` 1. Set the article's `archived` flag to be `false` 1. `$ maze exec 'a = Article.find(1); (a.archived = false) if a; a.save if a;'`

```text
# Be patient, it takes a few seconds - this is compiling your entire app
$ maze exec 'Article.find(1)'
#<Article:0x10c5f6700 @errors=[], @id=1, @title="Groundbreaking Ideas", @body="Just kidding, yet another self-important article.", @archived=true, @created_at=2017-11-14 14:13:39 UTC, @updated_at=2017-11-14 14:34:10 UTC>
# Those if statements are important, if you have a nilable type (Article | Nil)
$ maze exec 'a = Article.find(1); (a.archived = false) if a; a.save if a;'
true
# Notice the update `@archived=false`
$ maze exec 'Article.find(1)'
#<Article:0x10e640700 @errors=[], @id=1, @title="Groundbreaking Ideas", @body="Just kidding, yet another self-important article.", @archived=false, @created_at=2017-11-14 14:13:39 UTC, @updated_at=2017-11-14 14:35:06 UTC>
```

The history of your code, and the resulting output is saved in a `./tmp` directory:

```text
$ ls -l
1510698868787_console.cr
1510698868787_console_result.log
1510698901965_console.cr
1510698901965_console_result.log
1510698912435_console.cr
1510698912435_console_result.log

# Review the output of your actions
$ cat ./tmp/*result.log
#<Article:0x10c5f6700 @errors=[], @id=1, @title="Groundbreaking Ideas", @body="Just kidding, yet another self-important article.", @archived=true, @created_at=2017-11-14 14:13:39 UTC, @updated_at=2017-11-14 14:34:10 UTC>
true
#<Article:0x10e640700 @errors=[], @id=1, @title="Groundbreaking Ideas", @body="Just kidding, yet another self-important article.", @archived=false, @created_at=2017-11-14 14:13:39 UTC, @updated_at=2017-11-14 14:35:06 UTC>
```

## Editor Mode

Editor mode is activated by entering `maze exec` with no arguments. By default, editor mode will open the Vim text editor \(this can be overridden by specifying your preferred text editor as the `-e` option\). Once you are done editing your code, you can quit without saving to abort, or you can save and quit, which will cause maze to run the code. Specifying a value for the `--back` option allows you to go _n_ scripts back and edit+run that script.

### Example

```text
$ maze exec -e nano -b 1
(nano opens the previous script that was edited + run in editor mode)
(output of the script is printed to the terminal once you save + quit)
```

## File Mode

File mode is invoked in a similar to inline mode and it is executed in editor mode \(opening a terminal editor\).

The invocation, just pass a path to a crystal file, rather than a string to execute - `maze exec filename.cr`

The argument must be a string ending in .cr, and must correspond with a file that exists on the file system, within the current project.

The file then opens in edit mode. The changes you make will **not** modify the original source file, but they will be used when `maze exec` runs the code and saved as a `./tmp/{timestamp}_console.cr` file.

### Example

```ruby
# ./cool_stuff.cr
statement = "cool stuff happened"
emoticon = "^_^"
puts "#{statement} #{emoticon}"
```

```text
$ maze exec cool_script.cr
# vim or another editor opens
# make edits if necessary
# save the contents
cool stuff happened ^_^
```

