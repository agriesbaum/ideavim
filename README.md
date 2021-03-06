IdeaVim
=======

<div>
  <a href="http://teamcity.jetbrains.com/viewType.html?buildTypeId=IdeaVim_Build&guest=1">
    <img src="http://teamcity.jetbrains.com/app/rest/builds/buildType:(id:IdeaVim_Build)/statusIcon.svg?guest=1"/>
  </a>
  <span>Build<span>
</div>

<div>
  <a href="http://teamcity.jetbrains.com/viewType.html?buildTypeId=IdeaVim_TestsForIntelliJ15&guest=1">
    <img src="http://teamcity.jetbrains.com/app/rest/builds/buildType:(id:IdeaVim_TestsForIntelliJ15)/statusIcon.svg?guest=1"/>
  </a>
  <span>Tests</span>
</div>

IdeaVim is a Vim emulation plugin for IDEs based on the IntelliJ platform.
IdeaVim can be used with IntelliJ IDEA, RubyMine, PyCharm, PhpStorm, WebStorm,
AppCode, CLion, DataGrip and Android Studio.

Resources:

* [Plugin homepage](http://plugins.jetbrains.com/plugin/164)
* [Changelog](CHANGES.md)
* [Bug tracker](http://youtrack.jetbrains.com/issues/VIM)
* [Continuous integration builds](http://teamcity.jetbrains.com/project.html?projectId=IdeaVim&guest=1)
* [@IdeaVim](http://twitter.com/ideavim) in Twitter


Installation
------------

Use the IDE's plugin manager to install the latest version of the plugin.
Start the IDE normally and enable the Vim emulation using "Tools | Vim
Emulator" menu item. At this point you must use Vim keystrokes in all editors.

If you wish to disable the plugin, select the "Tools | Vim Emulator" menu so
it is unchecked. At this point your IDE will work with its regular keyboard
shortcuts.

Keyboard shortcut conflicts between the Vim emulation and the IDE can be
resolved via "File | Settings | Vim Emulation", "File | Settings | Keymap"
and key mapping commands in your ~/.ideavimrc file.


Summary of Supported Vim Features
---------------------------------

Supported:

* Motion keys
* Deletion/changing
* Insert mode commands
* Marks
* Registers
* Undo/redo
* Visual mode commands
* Some Ex commands
* Some [:set options](doc/set-commands.md)
* Full Vim regexps for search and search/replace
* Key mappings
* Macros
* Digraphs
* Command line and search history
* Window commands
* Vim web help

Emulated Vim plugins:

* vim-surround

Not supported (yet):

* Jump lists
* Various less used commands

See also:

* [List of recently added commands](src/com/maddyhome/idea/vim/package-info.java)
* [Top features and bugs](http://youtrack.jetbrains.com/issues/VIM?q=%23Unresolved+sort+by%3A+votes)


Files
-----

* ~/.ideavimrc
    * Your IdeaVim-specific Vim initialization commands

You can read your ~/.vimrc file from ~/.ideavimrc using this command:

    source ~/.vimrc

Note, that IdeaVim currently parses ~/.ideavimrc file via simple pattern matching,
see [VIM-669](http://youtrack.jetbrains.com/issue/VIM-669) for proper parsing
of VimL files.

Also note that if you have overridden the `user.home` JVM option, this
will affect where IdeaVim looks for your .ideavimrc file.  For example, if you
have `-Duser.home=/my/alternate/home` then IdeaVim will source
`/my/alternate/home/.ideavimrc` instead of `~/.ideavimrc`.


Emulated Vim Plugins
--------------------

IdeaVim extensions emulate some plugins of the original Vim. In order to use IdeaVim extensions, you have to enable
them via this command in your ~/.ideavimrc:

    set <extension-name>

Available extensions:

* surround
    * Emulates [vim-surround](https://github.com/tpope/vim-surround)
    * Commands: `ys`, `cs`, `ds`, `S`


Changes to the IDE
------------------

### Undo/Redo

The IdeaVim plugin uses the undo/redo functionality of the IntelliJ platform,
so the behaviour of the `u` and `<C-R>` commands may differ from the original
Vim. Vim compatibility of undo/redo may be improved in future releases.

See also [unresolved undo issues](http://youtrack.jetbrains.com/issues/VIM?q=%23Unresolved+Help+topic%3A+u).

### Escape

Using `<Esc>` in dialog windows remains problematic. For most dialog windows
the Vim emulator is put into the insert mode with `<Esc>` not working. You
should use `<C-c>` or `<C-[>` instead. In some dialog windows the normal mode is
on by default. The usage of the Vim emulator in dialog windows is an area for
improvements.

See also [unresolved escape issues](http://youtrack.jetbrains.com/issues/VIM?q=%23Unresolved+Help+topic%3A+i_Esc).

### Executing IDE Actions

IdeaVim adds two commands for listing and executing arbitrary IDE actions as
Ex commands or via `:map` command mappings:

* `:actionlist [pattern]`
    * Find IDE actions by name pattern
* `:action {name}`
    * Execute an action named `NAME`

For example, here `\r` is mapped to the Reformat Code action:

    :map \r :action ReformatCode<CR>


Contributing
------------

### Where to Start

In order to contribute to IdeaVim you should have some understanding of Java.

See also these docs on the IntelliJ API:

* [IntelliJ architectural overview](http://confluence.jetbrains.com/display/IDEADEV/IntelliJ+IDEA+Architectural+Overview)
* [IntelliJ plugin development resources](http://confluence.jetbrains.com/display/IDEADEV/PluginDevelopment)

You can start by picking relatively simple tasks that are tagged with
[#patch_welcome](http://youtrack.jetbrains.com/issues/VIM?q=%23patch_welcome)
in the issue tracker.


### Development Environment

1. Fork IdeaVim on GitHub and clone the repository on your local machine.

2. Import the project from existing sources in IntelliJ IDEA 15+ (Community or
   Ultimate) using "File | New | Project from Existing Sources..." or "Import
   Project" from the start window.

    * In the project wizard select "Import project from external model | Gradle"

    * Select your Java 6+ JDK as the Gradle JVM, leave other parameters unchanged

3. Create a new plugin run configuration using "Run | Edit Configurations | New
   Gradle Configuration" and run it in order to launch IntelliJ with the
   compiled version of the IdeaVim plugin.

    * Select your project as the Gradle project

    * Enter "runIdea" as the task to run

4. Create and run a new configuration for running tests by right-clicking on the
   "test" folder in the project structure and selecting "Run All Tests".

5. Build the plugin distribution by running `./gradlew clean buildPlugin` in the
   terminal in your project root.

    * The resulting distribution file is build/distributions/IdeaVim-VERSION.zip

    * You can install this file using "Settings | Plugins | Install plugin
      from disk"


Authors
-------

See [AUTHORS.md](AUTHORS.md)
for a list of authors and contributors.


License
-------

IdeaVim is licensed under the terms of the GNU Public license version 2.
