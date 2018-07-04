**bash-idh**: Bash Interactive Directory History
================================================

**bash-idh** enables Bash shell users to transparently view and interact
with Bash's built-in directory stack.  The interface is much cleaner and
much less cryptic than the built-in `dirs`, `pushd` and `popd` commands.

For example, if in a Bash session you've visited `/tmp`, `/usr/local/src`,
`/etc/init.d`, and `/home/user` (where your account name is `user`), the
built-in Bash command `dirs` will show (`~` indicates your home dir):

    /tmp /usr/local/src /etc/init.d ~

If you have enabled **bash-idh**, you'll get a prompt like: 

    <3> /tmp
    <2> /usr/local/src/
    <1> /etc/init.d
    [~ user@machine]$ 

and you can issue short commands to change the current directory to
places you've visited recently.  For example, given the above set of
recently visited directories, `back 3` will change the current directory
to the 3rd most recently visited directory (`/tmp`, labeled `<3>` in the
above directory history listing).

Enabling **bash-idh**
---------------------

To enable **bash-idh**, source `bash-idh.sh` from your `~/.bashrc` file.
For example:

    source /path/to/bash-idh.sh

**bash-idh** works in part by modifying the value of the `$PROMPT_COMMAND`
environment variable to call a function that prunes stale directories from
the Bash directory stack and then displays recently visited directories
above the prompt.

See the top of `bash-idh.sh` for customization possibilities.

**bash-idh** commands
---------------------

The commands below are intended to be issued from an interactive shell.

* `back`

   Navigate the directory history by giving this command followed by
   the number corresponding to a directory history entry to which
   you want to return.

   Usage: `back n` (where `n` is a directory history entry number)

   For example, `back 15` will change the current directory to the
   directory labeled as `<15>` in the directory history listing.

   `back` alone, with no `n`, is equivalent to `back 1`.

* `cd`

   This command overrides Bash's built-in `cd` command, to keep the
   directory stack from accumulating non-unique entries.  In every
   other respect, it works the same way as Bash's built-in `cd`.

* `drop`

   Use this command to remove individual directory history entries or
   ranges of them.

   Usage: `drop [n | n-m | -n | n- | all]`
   (where `n`,`m` are directory history entries)

   For example, `drop 15- 6 -2 8-12` will remove the following entries
   from the Bash directory stack (given that they exist):

   param  | removed entries
   -------|--------------------------------------------------
   `15-`  | 15 (and all entries with numbers greater than 15)
   `6`    | 6
   `-2`   | 1 and 2
   `8-12` | 8, 9, 10, 11 and 12

   `drop all` removes all directory stack entries.

* `tddh` ("Toggle display directory history")

   Use this command to toggle between three directory history lengths:
   max (default: 100 entries); moderate (default: 10 entries); and
   none.  This allows you to trade off screen real estate for
   immediate info about the Bash directory stack.

   The author uses the readline configuration file, `~/.inputrc`, to map
   the `[F9]` key to run this command (i.e. `"\e[20~":"tddh\n"`, under
   vt100 emulation).
