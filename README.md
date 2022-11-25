# better-terminal
A modern replacement for the command prompt.

I still use the command prompt a lot.
And I use modern tools, too.
It shouldn't be a choice.
I should be able to get some of the benefits of modern technology without (too many) legitimate complaints that it was easier in the good old days.

## Status

Rough ideas.

These are all doable.
But I'm still thinking through some of the details.
I'd love to build a few prototypes.

## Web Based

I've been heavily focused on JavaScript and HTML already.
And this seems like an ideal case for the technology.
I can run my same smart command prompt tool on a remote server as on my local machine.
As long as I can get an http connection, I can use a local GUI on whatever computer.

Think about hyperlinks.
You can move between machines just as quickly as you can move between directories.
One link will send you back to the same server and the other link will send you to a different server.
You might not even notice unless you were really paying attention.
That's how links were made to work!

## Local State

There's a lot that the nodejs server could do for you.
There's a lot that it could remember between one request and the next.
But why?

What if I close my laptop?
What if I open it in a different building?
Do I have to `cd` back into the right directory in every open Putty window?
Of course not, that's not how the web works.

More than that.
What if I want to open another window in the same directory as this window?
Shouldn't I be able to just copy the URL into a new window?
When I see a link to a different directory, shouldn't I have the option to open it in the current window or a new window?
These problems have been solved on the web.

## Top level layout

The main part of application is a command line.
You can type commands.

Other tools will be attached to help and will update as you type.

### Quick resizing

You will probably be using this alongside other applications.
And often you'll have two or more of these windows side by side.
This window needs to resize very easily.
That means quickly hiding the unused components as needed.

### Get out of my way

The other tools are on the side to be out of the way.
Think about auto completion.
As you are typing, the computer sometimes comes up with a list of suggestions.
And/or it gives you some relevant information about the code near your cursor.
The info is good, but where does the computer put it?
A typical IDE will draw that right on top of the the nearby code.

There's a whole section of my IDE dedicated to my `git` status and another listing all the files in my project.
These are always visible by default and they never get covered by anything.
But when I type code, the computer will cover the nearby code.

Put the helpful popups to the right of my code and put the output in another panel on the bottom.

Among other things, this allows those helpful popups to have a life of their own.
Imagine I'm typing code and I see help on the side.
Initially it's automatically highlighting the right part of the help as I type my code.
But it's just a normal help viewer, not a tiny attempt, so I can move my mouse over to that window and scroll and click even pop things out into their own window.

Same thing with the file selection tool.
If I'm typing the name of a file, a lot of shells have the option to show me possible completions.
Some are better than others, but they are all based on a text mode interface.
Let me type the commands as text, that's fine.
But if you're going to give me a list of files, why not show me a modern looking file manager?

And, again, the file manager can have real controls and a life of it's own.
I can move over there and inspect the entire directory.
Or I can move around, like a normal file open window.
Or I can pop this window out and have a normal file manger window, all without affecting the shell command I was in the process of writing.

And I can view lots of details about the files, while I'm typing the command.
I can see natural file manager stuff, like the size and date of each file, by default.
And I can right click to bring up a file in a new window, a file viewer window, without affecting my current work.

## File manager

The file manager panel will look a lot like a normal GUI file manager.
Like in Windows or OSX or similar.

It will have a list of files.
You can display them as icons or a table, maybe a table-tree for subdirectories.
You can sort the files by the usual fields.
You can search for files, both in this immediate list, and in all subdirectories, as a simple option.
You can select files.
You can copy the list of selected files to other applications, i.e. they are in some useful, non-proprietary format.
Etc.

Sometimes I only want to see this panel.
It should be easy for me to hide the other panels, e.g. the terminal text input.
It should be easy for me to restore the other panels.
I should be able to create a terminal from a file manager and vice versa.
Initially they should be linked.
But it should also be easy for me to duplicate one of the panels into a new unlinked window.

Normally the file manager and a terminal text input window are linked.
When I'm typing a file name, the file manager will go to the relevant directory,
and create a reasonable query, to show me what's possible.
But I can also take control from the file manager.
I can choose to move to a different directory or select a different set of files in this directory with the normal GUI gestures.

## History

Looking up old commands should be easier.
Once again, we're stuck with text mode tools.
But why?

The history should be available in a small window next to the main window.
It should be linked to the main window.
Certainly every time I type a new line it should be added to history.
And as I type the history window can try to guess what I want to see.

But I should be able to take over the history window, separate from the main window.
Maybe I want to search for something specific.
By default the command history might look for completions for what I've been typing.
But I can go into the history window and change the query.

In fact, the history window might look a lot like the file viewer window. 
I should be able to enter a series of regular expressions to filter out the list of lines.
And I should be able to use regular expressions to highlight parts of the text in color.

Most important, I should be able to easily copy and paste part of one line of history and part of another line of history onto the command I'm currently typing.


## Viewer
What are the main commands I use?  `wc`?  `cat`?  `less`?  `grep`?  `file`?  
Most of that needs to be replaced with a good file viewer.
Something with a scrollbar.

For the most part I'm looking at text UTF-8.
But it should be able to handle [ANSI escape sequences](https://en.wikipedia.org/wiki/ANSI_escape_code).
I hate having to choose between the colorful display that many commands give by default and the searching and scrolling options I get from `less`.
I should be able to do both at once!!!

As for bad characters, I probably need to see them all as numbers.
If it's weird or strange, I want details.

### Grep

Regular expression search should be easy.
I should be able to add a series of filters with just the click of a button.
Show me only the lines that match this query,
or only the lines that don't.
Or show me everything, but apply a color to things that match this query.
A series of these, not just one.
And it's all built into the viewer, so I get my scroll bar, etc.

### Awk

These should be nice ways to integrate the viewer with code.
The code would all be JavaScript.
But some of the ideas would come from awk.
Like feed me a file, or the output of that last command, one line at a time.
And display the output of this code in a viewer.
And a few relevant tools, like break up the line into fields.

This is all aimed at quick and dirty work.
Queries that I'm writing as I go.

## Pipes and Notebooks

It should be easy to create complicated series of commands.
Consider a typical command
```
cat my file|grep for something | sort --unique |wc
```
I should be able to build that up slowly, easily checking the result at each phase.

Select the file from the file manager, unless you just want to type `cat`.
You'll see details about the file in the file manager.
And maybe as soon as you click on it you see it in the file viewer.
Like a lot of modern guis.

You can start the grep in the file viewer,
then export the result to another process.
Or you can export the instructions from the GUI back to the command line, so you can add them to a script.

Alternatively, you can start with some complicated line of shell code, and when it doesn't work, you can easily insert a viewer into the middle of one of the pipes.

Most of all, you have the ability to see a lot of intermediate results, as you build up something bigger.

