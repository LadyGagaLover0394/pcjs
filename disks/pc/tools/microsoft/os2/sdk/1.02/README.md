---
layout: page
title: Microsoft OS/2 SDK 1.02
permalink: /disks/pc/tools/microsoft/os2/sdk/1.02/
---

Microsoft OS/2 SDK 1.02
---

This copy of the Microsoft OS/2 SDK (1.02) was obtained from the [WinWorld](https://winworldpc.com/product/os-2-1x/10)
website.  Unfortunately, it's missing the **NETWORK** disk, so we've included an empty **NETWORK** disk
that allows the SDK installation script to finish.

This SDK was released around December 1987 and included a copy of Microsoft OS/2 1.0.  We do not have any of the
printed documentation that came with the SDK, such as the *Installation Guide*, but we do have the
[Microsoft® Operating System/2 Programmer’s Toolkit](/docs/os2/microsoft/ptk/1.0/) from March 1988, thanks to the
[OS/2 Museum](http://www.os2museum.com/).

### Installation

If you look at the **TOOLKIT1** disk, in the **OS2DOC** folder, you'll find **READ.ME!**, which includes some very
useful information about the SDK installation process:

	The installation guide is confusing, can you give me three easy steps to
	installing the SDK?
	
		Sure.  First, put the program diskette into your machine and reboot it.
		Follow the instructions.  If you have a new machine, first format the
		hard drive, then reboot with the program diskette.
	
		Second: copy the files \OS2DOC\INPUT.EXE and \OS2DOC\INSTSDK.CMD from the
		TOOLKIT diskette to the root of your hard drive.  Run the program INSTSDK
		and answer its questions.
	
		Thats, all. [sic]

One of the first questions that the INSTSDK.CMD script asks is:

	Are you installing MS OS/2 SDK on a PS/2 machine?

PCjs currently only simulates PC, XT and AT-class machines, not PS/2 machines, so you might be inclined to answer
**NO** to that question, but in fact, the correct answer is **YES**, because the SDK doesn't actually care what kind
of machine you're using.  It's asking that question merely to determine whether you're using 3.5-inch or 5.25-inch SDK
distribution diskettes.  These disks happen to be the 3.5-inch versions, so you must pretend you're using a PS/2.

Also, this SDK may have only been tested with Microsoft's release of OS/2 1.0 (included with the SDK), because if you
install it on [IBM OS/2 1.0](/disks/pc/os2/ibm/1.0/), the script will fail when it attempts to run LIBBUILD to build
all the C runtime libraries.  Apparently, this is because IBM OS/2 1.0 creates an OS2INIT.CMD with PATH set to:

	C:\;C:\OS2;C:\OS2\INSTALL;

so when INSTSDK.CMD updates the PATH, it appends its own directories with a leading semi-colon, resulting in:

	C:\;C:\OS2;C:\OS2\INSTALL;;C:\OS2SDK\TOOLS\BIN;C:\OS2SDK\TOOLS\PBIN

and the "double semi-colon" apparently causes PATH searches to terminate prematurely, so the LIBBUILD program will
not be found.

To complete the SDK installation, fix the PATH in OS2INIT.CMD, then type the following command:

	for %i in (s m c l) do libbuild %i em %LIB%

and *now* your MS OS/2 SDK should be fully installed.  Well, not *quite* fully, because you won't have the files from
the missing **NETWORK** disk; specifically:

	IPCCALLS.DLL
	IPCCALLS.LIB
	IPCTEST.C
	LANMAN.INI
	MAILSLOT.H
	MAKEFILE
	NAMPIPE.SYS
	NMPIPE.H
	README.DOC

but you aren't likely to need those.

### Using SDKED

As previously noted, we don't have a copy of this SDK's documentation.  But we do have a copy of the "[User's Guide
to the Z Editor](/disks/pc/tools/microsoft/misc/root/Z.TXT)", by Mark Zbikowski, August 4, 1986, included
below.  **SDKED** was an OS/2 port of the Z Editor.








                                          .

       

       

       

       

       

                             User's Guide to the Z Editor

                                    Mark Zbikowski

                                    4 August 1986


















































                                  Table of Contents

       
       Starting Z..................................................... 1
       Editing Functions.............................................. 4
       Editing Switches and Flags.................................... 15
       Keystroke Macros.............................................. 17
       Index......................................................... 21
       Revision History.............................................. 23

       


















































       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM




                                What is the Z editor?

       Z is an editor, a program for creating and altering files.

       The editor creates the file specified or copies an existing file from
       disk into memory.  Then when the file is "saved", the copy in Z
       overwrites the copy on disk. The copy that was overlayed may be
       retrieved with the UNDEL command (see UNDEL.HLP and also the "backup"
       switch below).

       Z makes your screen into a window on the file you are editing.  The
       window can move forwards or backwards to any point in the file.  The
       cursor identifies the focus of each edit operation.

       The simplest editing operation is to move the cursor to the place you
       want to change and start typing characters.  What you type is stored in
       the corresponding location in the copy of the file in Z.  If you are in
       INSERT mode, then the characters you type are inserted at the cursor
       location instead of overwriting what is already there.

       The editor interprets ASCII control characters and some ASCII character
       sequences as commands.  Each control character has an editing command
       associated with it. You can change the association between editor
       commands and control characters or character sequences with the <switch>
       command.


                                      Starting Z

       Z uses several environment variables during its start-up.  First, Z
       looks for a file called TOOLS.INI by searching all the directories
       contained in the USER environment variable.  Contained in this TOOLS.INI
       file are any customizations you wish to make to the editor function
       assignments and editor switch settings. This file is optional.  Starting
       Z with the /D switch prevents TOOLS.INI from being read.

       Z uses a scratch file during it execution.  Normally, this file (Z.VM)
       is created in the root directory on the default drive when Z is started.
       If you want this file to be created elsewhere, for example on a ram-
       drive, you may use the TMP environment variable to direct Z to place it
       elsewhere.  The TMP variable is also used to locate other temporary
       files that Z uses.

       The TOOLS.INI file is used to maintain configuration information.  The
       files are divided into sections by tags which are the name of a tool
       surrounded by square brackets.  In the case of the Z editor, the
       following tags are used:

         [z]     following this tag should be general Z initialization

         [z-x.y] following this tag should be Z initialization peculiar to a
                 particular version of MSDOS.









       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


       For a sample of user initialization, see the TOOLS.INI file.

       The definitions in these files have one of several forms.  Below are the
       forms and a description of each.

         NAME=xx yy zz...

       This assignment directs Z to view the sequence of characters xx yy zz
       ... (in hexadecimal) as a single keystroke.  This is often used for
       naming function keys on your terminal.

         NAME="chars"

       Similar to the previous form except that the characters are named
       explicitly. Quotes may be preceded with the "\" character to allow you
       to enter them directly.

         function:=function1 function2...

       Defines a new function in terms of existing functions.  This is called a
       MACRO. When the new function is executed by Z, each function contained
       in the definition is executed in order.  Further information is
       contained in the Keyboard Macros section below.

         function:keys

       Causes Z to execute the named function when the specified keys are read
       from the keyboard.  The keys are either a key name as defined above or a
       sequence of characters to be used.  Note that ^X in such a sequence
       stands for CONTROL-X rather than up-arrow-X.  You may have several keys
       or key sequences assigned to a particular editing function, but you may
       have ONLY one function on a key or sequence.  A description of the
       available editing functions is below.

         switch:value

       Set a particular configuration switch in Z to a value.  See the
       "switches and flags" section below for more information.

       Anyway, when Z is through initializing, it attempts to read the file
       specified on the command line.  If Z was invoked without an argument, it
       will attempt to read in the most recently edited file.

       When the file has been read in, Z will display the file on the top 23
       lines of the screen.  The bottom two lines are used as follows:

            The 24th line is used as a dialog line.  Prompts and messages
            appear on this line.

            The 25th line is used as a status line.  The information that
            appears is (from left-to-right):

            filename of file being edited 
            type of file (a guess based on the extension)     



                                        - 2 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


            the word modified, if you have changed the file   
            the length in lines of the file    
            the position in (row, column) form of the upper-left corner of the
            screen relative to the first byte of the file.  (1,1) is the top of
            the file

       Now for the interesting part.  Normally, when a key sequence is
       recognized by Z as being attached to an editing function, Z will execute
       that function.

       Most functions have a 'default' action which is unchangeable.  You may
       change this action by preceding the editing function with an argument
       and/or a mode- function modifier.

       Arguments are introduced by the <arg> editor function.  When you enter
       the <arg> function, Z will reverse the video at the current cursor
       position. You may then enter the argument as follows:

         A sequence of cursor movements:

            If the cursor ends up on top of the <arg> then the argument is
                 called a nullarg and represents either the remainder of the
                 line up to (and possibly including the line break) or
                 represents the next space-terminated word on the line
                 depending on the editing function.

            If the cursor ends up on the same line but on a different column,
                 the argument is called a streamarg and represents all text
                 from the leftmost of the <arg> and cursor up to one character
                 position to the left of the rightmost of the <arg> and cursor.

            If the cursor ends up in the same column as the <arg> then the
                 argument is called a linearg and represents the range of lines
                 beginning with the line that contains the <arg> up to and
                 including the line that contains the cursor.

            If the cursor ends up on a different line and column from the
                 <arg>, the arg is known as a boxarg and may represent either a
                 rectangle of text whose diagonal is delimited by the <arg> and
                 cursor or the sequence of characters beginning at the
                 uppermost of <arg> and cursor through the bottommost of <arg>
                 and cursor including the line breaks.  This distinction is
                 made by the editing function itself.

         You may also type normal characters.  You are prompted, on the dialog
         line, to enter an argument.  The types of textual arguments are:

            ASCII text.  This is called a textarg.  The argument to the
                 function is merely the text you have typed.

            A number.  This is called a numarg and is the same as if you had
                 moved the cursor either upward or downward the specified
                 number of lines.




                                        - 3 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


            A bookmark.  This is called a markarg.  This is the same as if you
                 had moved the cursor to the bookmark position.  To define a
                 bookmark, see the <mark> command.

       The only mode-command modifier at the present is the <meta> command.
       Its effect on each function is described in that function's description.


                                  Editing Functions

       Here is the current set of Z functions with a description of the allowed
       arguments and a description of how they affect the command's operation.
       Also, in each function description is the default assignment.

       <arg> (^X) introduces an argument to modify a subsequent operation.  To
         cancel an  <arg>, enter the <cancel> command.  There are no modifiers
         or arguments allowed for this command.

       <assign> (^^) makes a Z configuration change.  An argument MUST be
         specified and be of the form described for TOOLS.INI above:

         <arg>linearg<assign> treats each line as a separate assignment or key
            definition.

         <arg>textarg<assign> treats textarg as an assignment or a key
            definition.

         <arg>nullarg<assign> treats the remainder of the line to the right of
            the cursor but not including the line break as an assignment or a
            key definition.

         <arg>streamarg<assign> treats the outlined text as an assignment or a
            key definition.

         The special case of <arg>?<assign> displays all the current keyboard
         assignments.

       <backtab> (SHIFT-TAB) is a cursor movement function.  It will move the
         cursor leftward to the next tabstop.  Tabstops are defined to be every
         nth character where n is settable by the tabstops editor switch.
         Being a cursor movement function, <backtab> takes no arguments nor
         mode-command modifiers.

       <begline> (END) is a cursor movement function that places the cursor on
         the first non-blank character on the line.

         <meta><begline> places the cursor on the first character position on
            the line regardless of the contents of the line.

       <cancel> (^C) will cancel the current operation in progress.  Depending
         on your operating system, some of these operations may be completed
         before the <cancel> is read.  <cancel> will always cancel an argument
         so it never takes an argument nor a mode-command modifier.




                                        - 4 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


       <cdelete> (BACKSPACE or ^H) will attempt to delete the previous
         character. Note that this function will NOT delete line breaks.  For
         that function, see the <emacscdel> function below.  If the cursor is
         in column 1, <cdelete> will move the cursor to the previous line and
         place it just to the right of the last character on that line.  If
         issued while an argument was being issued, <cdelete> is treated as a
         cursor-left command.  If issued in insert mode, <cdelete> will delete
         the previous character from the line, reducing the length of the line
         by 1.  If there is nothing but whitespace on the line to the left of
         the cursor, the cursor is placed in column 1 of the line.  If the
         cursor is beyond the last non- whitespace character on the line, it is
         moved to the character immediately to the right of the end of line.
         Otherwise, the cursor is moved one position to the left and a space
         replaces the character under the cursor.

       <compile> (^U) is used to perform background compilations and to review
         error messages from them.

         <compile> will read the next error message and attempt to parse it
            into file, row, column and message.  If it is successful, Z will
            read in the file, place the cursor on the appropriate row and
            column, and display the message on the dialog line.  <compile>
            currently works with GREP, Lattice C, Microsoft C, and the C-based
            Microsoft Assembler.

         <meta><compile> will read error messages and advance to the first
            message that is NOT for the current file.

         <arg>nullarg<compile> will attempt to compile the current file,
            resulting in the current file being compiled and linked.  The
            command and arguments used to compile the file are determined by
            the extension of the file and can be changed by the extmake: switch
            .

         <arg>textarg<compile> uses a special command and arguments to compile
            the specified text.  This can be changed by using the extmake:
            switch with extension "text".

         <arg>streamarg<compile> as above but uses the text selected on the
            screen as the arguments for the command.

         <arg><arg>textarg<compile> will invoke the text as a program.  The
            program is assumed to display its errors in file row column message
            format. This is often useful to find text in a series of files by
            using GREP:
                 grep /l pat files   ; zibo grep
                 grep -n pat files   ; *NIX grep

       <curdate>  (ALT-D) is a predefined macro that will insert the current
         date at the current cursor position.

       <curday> is a predefined macro that will insert the current day at the
         current cursor position.




                                        - 5 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


       <curfileext> is a predefined macro that is the extension of the most
         recently switched file.

       <curfilenam> is a predefined macro that is the file name of the most
         recently switched file.

       <curtime>  (ALT-T) is a predefined macro that will insert the current
         time at the current cursor position.

       <curuser> is a predefined macro that will insert the name of the current
         user at the current cursor position.  This uses the MAILNAME
         environment variable.

       <down> (DOWN arrow) is a cursor movement function that moves the cursor
         to the line below the current one.  If this results in the cursor
         moving off the bottom of the screen, the window is adjusted
         appropriately.  Being a cursor movement function, <down> takes no
         arguments.

         <meta><down> moves the cursor to the same column position but to the
            last displayed line on the current window.

       <emacscdel> (CTRL-BACKSPACE) behaves identically to <cdelete> except
         that at the beginning of a line while in insert mode, <emacscdel> will
         delete the line break between the current line and the previous line,
         joining the two lines together.

       <emacsnewl> (unassigned) behaves identically to <newline> except that
         when in insert mode, it will break the current line at the current
         cursor position.

       <endline> (PGDN) moves the cursor beyond the last character on a line.

         <meta><endline> moves the cursor to the column corresponding to the
            right- most edge of the screen.

       <exit> (F9) is used to terminating an editing session.  There are
         editing flags and switches that modify the behaviour of the <exit>
         command: askexit/noaskexit, backup, entab, tmpsav (see Editing
         Switches and Flags section).

         <exit> saves the current file if it has been modified.  Z saves its
            temporary file and scans the set of in-core files.  If any are
            modified, Z will ask you to confirm the exit.

         <meta><exit> is identical to <exit> except that it skips the save of
            the current file.  See <setfile> for details of the saving
            operation.

         <arg><exit> is identical to <exit> except that Z does not exit but
            advances to the next file on the command line.

         <arg><meta><exit> is identical to <arg><exit> except that Z does not
            save the current file.



                                        - 6 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


       <home> (HOME) is a cursor movement function that places the cursor in
         the upper-left-hand corner of the current window.

       <information> (F1) saves the current file and <setfile>'s to the
         information file which contains a list of all files in core along with
         the current set of files that you have edited.  The size of this list
         is controlled by the tmpsav switch.

       <initialize> (F2) causes Z to reread the user configuration files. This
         is useful when initially configuring your editor and when attempting
         to use someone else's keyboard assignments.

         <initialize> rereads all the Z switches for the user configuration
            files.

         <arg>text<initialize> rereads all the Z switches for the system and
            reads the user switches from the section of the user's TOOLS.INI
            that is tagged [Z- text].

       <insertmode> (^N) toggles the state of the insert mode switch.  This
         switch is easily seen on the right hand side of the status line.  When
         insert mode is on, each graphic character is inserted at the current
         cursor position, the remainder of the line is shifted one character to
         the right and the cursor is advanced one position.  Note, however,
         that the <newline> function is NOT a graphic character and does NOT
         cause insertion of a line break.  For this, please see the <emacsnewl>
         function.  Z normally is started in overstrike mode.  You can use the
         editor flag enterinsmode to cause Z to begin execution in insert mode.

       <ldelete> (^F) deletes a range of lines or a box within a series of
         lines.

         <ldelete> deletes the current line and places it into the pick buffer.

         <arg><ldelete> deletes from the cursor up to the end of line and
            places that text into the pick buffer.  Note that it does not join
            the current line with the next line.

         <arg>linearg<ldelete> deletes all lines specified and places the block
            into the pick buffer.

         <arg>boxarg<ldelete> deletes the box specified from the file and
            places it into the pick buffer.

         <arg>streamarg<ldelete> deletes the specified characters (treated as a
            box one line high).

       <left> (LEFT arrow) moves the cursor one position to the left.  If this
         results in the cursor being off the screen, then the window is
         adjusted appropriately by scrolling a number of columns defined by the
         hscroll editor switch.

         <meta><left> moves the cursor to the leftmost position on the screen.




                                        - 7 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


       <linsert> (^D) inserts blank lines.

         <linsert> inserts one blank line underneath the cursor.

         <arg><linsert> inserts or deletes blanks at the beginning of a line to
            make the first non-blank character appear under the cursor.

         <arg>linearg<linsert> inserts the indicated range of blank lines.

         <arg>boxarg<linsert> inserts an empty box in the indicated range.

         <arg>streamarg<linsert> inserts an empty region (treated as a box one
            line high).

       <mark> (^P) goes to a specified spot in a file.

         <mark> goes to beginning of file.

         <arg><mark> restores the screen to its previous location.  Z remembers
            only one previous location.  <arg><mark> is used to flip between
            two viewpoints in the file.

         <arg>numarg<mark> moves the cursor to the beginning of the specified
            line.

         <arg><arg>text<mark> defines a bookmark at the current cursor
            location. That bookmark can now be addressed with the specified
            textual name.

         <arg>text<mark> moves the cursor to the indicated bookmark.  If it was
            not previously defined, Z will use the editor switch markfile to
            find a file that contains bookmark definitions.  This file contains
            lines of the form: bookmark file row column

       <meta> (ESC) is a function modifier.  It is used to prefix functions to
         change their behaviour.  See the individual function description for
         more information.

       <mlines> (^W) adjusts the window on the file a few lines towards the
         beginning of the file.

         <mlines> adjusts the window backwards in the file.  The number of
            lines it is moved is determined by the editor switch vscroll.

         <arg><mlines> moves the window until the line that the cursor is on is
            at the bottom of the screen.

         <arg>numarg<mlines> moves the window backwards the specified number of
            lines.

       <mpage> (^Q) moves the window back by pages.

         <mpage> moves the window backwards in the file by one screen's worth
            of lines.



                                        - 8 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


         <arg><mpage> moves the window all the way back to the beginning of the
            file.

         <arg>numarg<mpage> moves the window the specified number of pages
            backward in the file.

       <mpara> (CTRL-PGUP) moves the cursor backwards by paragraphs.
         Paragraphs are blocks of text separated by blank lines.

         <mpara> moves the cursor backwards one paragraph and places the cursor
            on the first line of the paragraph

         <meta><mpara> moves the cursor backwards one paragraph and places the
            cursor just beyond the last line of the paragraph.

       <msearch> (^E) searches backwards in a file for a string or a regular
         expression. If the editor switch case is set then case is significant
         in the search otherwise case is ignored.

         <msearch> searches backwards for the previously defined string or
            pattern. If the string/pattern is found, then the window is moved
            to display it and the matched string/pattern is highlighted.  If it
            was not found, no cursor movement takes place.

         <arg>streamarg<msearch> searches backwards for the selected text.  In
            this case, the text is treated as a simple string.

         <arg>text<msearch> searches backwards for the text.  In this case, the
            text is treated as a simple string.

         <arg><arg>streamarg<msearch>
         <arg><arg>text<msearch> searches backwards for a regular expression.

         The patterns that Z understands are called "regular expressions".
         These are true regular expressions (plus some optimizations) rather
         than the much-weakened form that is used on the *NIX xGREPs.

         The simplest form of regular expression is just a string, like
         "hello". This pattern will match occurrences of the word "hello", or
         substrings of words like "othello".  It will even match the string
         "Hello" if the nocase editor switch is given.  Most characters in a
         regular expression match themselves, but some characters (one of
         "{}()[]!~:?^$+*@#") have a special meaning to the pattern matcher.
         These special characters are used to specify more complex patterns:

         \  "escape"; ignore the special meaning of the next character and just
            match that character.  "\?" matches the question-mark and "\\"
            matches a single backslash.

         ?  "wildcard";  match any character.

         [class]  "character class";  this is used to match one of a set of
            characters. "[abc]" matches an "a", "b", or "c".  The character "-"




                                        - 9 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


            is used here to specify a range of characters; "[a-zA-z0-9]"
            matches a letter or a number.

         [~class]  "not character class"; this is used to match a character
            that is NOT in the specified set of characters.

         ^  "beginning of line";  this matches or "anchors" a pattern to the
            beginning of the line.

         $  "end of line";  matches the end of a line.

         In the following, X denotes some regular expression:

         X* "closure";  this matches zero or more occurrences of the pattern X.
            It will match as few X's as it can, e.g. if the pattern is "?*ab"
            then it will match the first "ab" in "abababab".  If the pattern is
            "?*ab$", then it will match the entire string "abababab", with the
            "?*" portion of the pattern matching "ababab".

         X+ "plus"; this is just a shorthand for XX+.  It will match one or
            more occurrences of the pattern X.

         X@  "greedy closure"; this matches zero or more occurrences of the
            pattern X, but it starts out by matching as many X's as it can. and
            backs off on this choice ONLY if the rest of the pattern doesn't
            match.  So, the pattern "?@ab" will match the whole string
            "abababab", unlike "?*ab" above.

         X# "greedy plus";  a shorthand for XX@.

         (X1!X2!...!Xn)  "alternation";  this will match either X1, or X2, ...
            or Xn. It tries them in that order and it will switch from Xi to
            Xi+1 only if the rest of the pattern fails to match.

         ~X "not" or "guard";  this pattern matches nothing, but it checks to
            see if the string matches X at this point, and fails if it does.
            For example, "^~(foo!bar)?*$" will match all lines that don't begin
            with "foo" or "bar".

         X^n  "power";  this pattern matches exactly n copies of X.

         The following commonly used patters are defined for your typing
         convenience. To use them, just put :<letter> in your pattern:

            :a   [a-zA-Z0-9]                   alphanumeric
            :b   ([ \t]#)                      whitespace
            :c   [a-zA-Z]                      alphabetic
            :d   [0-9]                         digit
            :f   ([~ "\[\]\:<|>+=;,.]#)        file part
            :h   ([0-9a-zA-Z]#)                hex number
            :i   ([a-zA-Z_$][a-zA-Z0-9_$]@)    identifier
            :n   ([0-9]#.[0-9]@![0-9]@.[0-9]#![0-9]#)    number
            :p   (([a-z]\:!)(\\!)(:f(.:f!)\\)@:f(.:f!))  path
            :q   ("[~"]@"!'[~']@')             quoted string



                                       - 10 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


            :w   ([a-zA-Z]#)                   word
            :z   ([0-9]#)                      integer

       <mword> (unassigned) moves the cursor backwards by words.

         <mword> moves the cursor backwards one word and places the cursor on
            the beginning of the word.

         <meta><mword> moves the cursor backwards one word and places the
            cursor just beyond the end of the word.

       <newline> (ENTER or ^M) moves the cursor to a new line.

         <newline> moves the cursor to the beginning of the next line.  If the
            editor switch softcr is set, then Z will attempt to place the
            cursor on a meaningfully tabbed-in position based on the type of
            file. If the file is a C program, then Z will attempt to correctly
            tab in based on continuation of lines and on open blocks.
            Otherwise, if the next line is blank, Z will place the cursor in
            the column corresponding to the first non-blank character in the
            previous line.  If all else fails, Z places the cursor on the first
            non-blank character of the line.

         <meta><newline> moves the cursor to the real beginning of the next
            line.

       <pbal> (^V) balances parenthesis and brackets.

         <pbal> scans backwards through the file balancing parenthesis and
            brackets. When the first unbalanced one is found, the matching
            character is placed into the file at the cursor position. If it is
            found in the visible window, Z will alter its color for a short
            interval.  If it is found and it is not visible, Z will display the
            matching line on the dialog line.

         <arg><pbal> scans forward for unbalanced characters.

       <pick> (^K) grabs text from the file and places it into the pick buffer.
         This allows simple copy-and-paste operations.

         <pick> places the current line into the pick buffer.

         <arg><pick> places the text from the current cursor position up to the
            end-of- line into the pick buffer.  Note that the line break is not
            picked up.

         <arg>linearg<pick> places the specified range of lines into the pick
            buffer.

         <arg>boxarg<pick> places the text of specified box into the pick
            buffer.

         <arg>text<pick> places the text into the pick buffer.




                                       - 11 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


         <arg>numarg<pick> places the specified range of lines into the pick
            buffer.

         <arg>markarg<pick> places the range of text between the cursor and the
            location of the bookmark into the pick buffer.

       <plines> (^T) adjusts the window on the file a few lines towards the end
         of the file.

         <plines> adjusts the window forward in the file.  The number of lines
            it is moved is determined by the editor switch vscroll.

         <arg><plines> moves the window until the line that the cursor is on is
            at the top of the screen.

         <arg>numarg<plines> moves the window forward the specified number of
            lines.

       <ppage> (^L) moves the window forward by pages.

         <ppage> moves the window forwards in the file by one screen's worth of
            lines.

         <arg><ppage> moves the window all the way to the end of the file.

         <arg>numarg<ppage> moves the window the specified number of pages
            forward in the file.

       <ppara> (CTRL-PGDN) moves the cursor forwards by paragraphs.  Paragraphs
         are blocks of text separated by blank lines.

         <ppara> moves the cursor forwards one paragraph and places the cursor
            on the first line of the paragraph

         <meta><ppara> moves the cursor forwards one paragraph and places the
            cursor just beyond the last line of the paragraph.

       <psearch> (^R) searches forwards in a file for a string or a regular
         expression. See <msearch> for the definition of the regular expression
         patterns.

         <psearch> searches forwards for the previously defined string or
            pattern. If the string/pattern is found, then the window is moved
            to display it and the matched string/pattern is highlighted.  If it
            was not found, no cursor movement takes place.

         <arg>streamarg<psearch> searches forwards for the selected text.  In
            this case, the text is treated as a simple string.

         <arg>text<psearch> searches forwards for the text.  In this case, the
            text is treated as a simple string.

         <arg><arg>streamarg<psearch>
         <arg><arg>text<psearch> searched forwards for a regular expression.



                                       - 12 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


       <push> (^Z) runs the command shell.  Depending on the OS, you either get
         COMMAND.COM or SH.

         <push> saves the current file and runs the shell.

         <meta><push> does not save the current file and runs the shell.  See
            <setfile> for a description of the save operation.

         <arg><push> uses the text on the screen from the cursor up to end-of-
            line as a command to the shell.

         <arg>text<push> uses the text as a command to the shell.

       <put> (^G) inserts the text of the pick buffer into the file beginning
         at the current cursor position.  The insertion depends on the type of
         text stored in the pick buffer:

         <arg>text<put>

       <arg>streamarg<put> places the specified text into the pick buffer and
       inserts the specified text at the current cursor position.

         <arg><arg>text<put> interprets text as a filename and will insert the
            contents of the specified file into the current file at the current
            cursor position.

         lines are inserted directly before the cursor and do not break the
         line. boxes are inserted in the current line and all succeeding lines.
         streams break the current line and are inserted at the cursor.

       <pword> (unassigned) moves the cursor forwards by words.

         <pword> moves the cursor forwards one word and places the cursor on
            the beginning of the word.

         <meta><pword> moves the cursor forwards one word and places the cursor
            just beyond the end of the word.

       <qreplace> (CTRL-ENTER or ^J) performs global search and replace but
         prompts for confirmation of each replacement.  See <replace>.

       <quote> (unassigned) reads one keystroke from the keyboard and treats it
         literally. This is useful for inserting text into a file that happens
         to be assigned to an editor function.

       <refresh> (F10) reloads or discards the current file.

         <refresh> prompts and rereads the file from disk, discarding all
            edits.

         <arg><refresh> prompts and discards the file from the editor memory.

       <replace> (^O) performs global search and replace.  The editor switch
         case indicates whether case is significant for comparison.



                                       - 13 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


         <replace>
         <arg><replace>
            perform simple search and replace, prompting you for the search
            string and for the replacement string.  The search begins at the
            cursor position and continues through the end of file.

         <arg>linearg<replace> performs the search and replace on the specified
            line range.

         <arg>numarg<replace> performs the search and replace on the specified
            line range.

         <arg>boxarg<replace> performs the search and replace within the
            specified box.

         <arg>markarg<replace> performs the search and replace between the
            cursor and the specified bookmark.

         <arg><arg><replace>
         <arg><arg>linearg<replace>
         <arg><arg>numarg<replace>
         <arg><arg>boxarg<replace>
         <arg><arg>markarg<replace>
            all perform the same as above except that the search pattern is a
            regular expression and the replacement pattern can select special
            tagged sections of the search for selective replacement.  If the
            regular expression contains {...} these are not matched directly
            (except when preceded with a \).  They indicate the beginning and
            end of tagged sections.  You can select from these in the
            replacement string by $n where n is a digit from 0 to 9.  $0
            represents the entire matched string.  For example, if the pattern
            is

            "^{[a-zA-Z]@} #{[0-9]@}$"
         
            and the string is "Fahrenheit 451", the first pair of curly braces
            will mark off "Fahrenheit", and the second pair will delimit "451".
            You can refer to the first field as $1, the second as $2, and the
            whole matched string as $0.

       <restcur> is a predefined macro that restores the current cursor
         position saved with <savecur>.

       <right> (RIGHT arrow) moves the cursor one position to the right.  If
         this results in the cursor being off the screen, then the window is
         adjusted appropriately by scrolling the number of columns specified by
         the hscroll editor switch.

         <meta><right> moves the cursor to the rightmost position on the
            screen.

       <savecurs> is a predefined macro that saves the current cursor position
         to be restored with <restcur>.




                                       - 14 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


       <sdelete> (^S) deletes a stream of text.  This includes line breaks and
         parallels what simpler editors (vi, emacs) do.

         <sdelete> delete one character under the cursor.  This does not delete
            line breaks.  It does not place that character into the pick
            buffer.

         <arg><sdelete> delete from the cursor through the end-of-line, joining
            the following line with the current line the cursor position.  The
            text deleted (including the line break) is placed into the pick
            buffer.

         <arg>streamarg<sdelete> delete the indicated stream of text.

         <arg>linearg<sdelete>
         <arg>boxarg<sdelete>
         <arg>markarg<sdelete> delete the text beginning at the bookmark and
            ending at the cursor including all line breaks.  All removed text
            is entered into the pick buffer.

       <setfile> (^B) switches the file currently being edited, optionally
         saving any changes to the current file. If the name of the file you
         indicate contains any meta-characters (? or *) Z will display a menu
         of all matching files.  If the file to be save is read-only, Z will
         prompt you for another name under which to save the file.  Z will also
         allow you to specify a environment variable as part of the name to be
         searched.  For example, if you have a batch file FOO.BAT somewhere in
         your execution path, you can use <setfile> to visit it by entering
         <arg>$PATH:FOO.BAT<setfile>.

         <setfile> switches to the most-recently edited file saving any
            changes. Toggling between two file is accomplished by repeated
            <setfile>'s.

         <arg><setfile> switches to the file name that begins at the cursor and
            ends on the first blank, saving any changes made to the current
            file.  If the text indicated is in actuality a directory, Z will
            change its working directory to that specified.

         <arg>text<setfile> switches to the specified text. If the text
            indicated is in actuality a directory, Z will change its working
            directory to that specified.

         <meta><setfile>
         <arg><meta><setfile>
         <arg>text<meta><setfile> as above but disables the saving of changes
            to the current file.

         <arg><arg>text<setfile> saves the current file under the specified
            name.

         <arg><arg><setfile> saves the current file.

       <setwindow> (^]) redisplays the screen and adjusts the window.



                                       - 15 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


         <setwindow> redisplays the entire screen.

         <meta><setwindow> redisplays the line that the cursor is on.

         <arg><setwindow> adjusts the window so that the cursor position is in
            the upper left.

       <sinsert> (^A) inserts streams of blank space.

         <sinsert> inserts a single blank space.

         <arg><sinsert> inserts a line break at the current cursor position,
            splitting the line at the cursor.

         <arg>linearg<sinsert>
         <arg>boxarg<sinsert>
         <arg>markarg<sinsert> break the line at the bookmark and insert the
            appropriate number of blank lines and spaces.

       <tab> (TAB or ^I) is a cursor movement function.  It will move the
         cursor rightward to the next tabstop.  Tabstops are defined to be
         every nth character where n is settable by the tabstops editor switch.
         Being a cursor movement function, <tab> takes no arguments nor mode-
         command modifiers.

       <up> (UP arrow) is a cursor movement function that moves the cursor to
         the line above the current one.  If this results in the cursor moving
         off the top of the screen, the window is adjusted appropriately.
         Being a cursor movement function, <up> takes no arguments.

         <meta><up> moves the cursor to the same column position but to the top
            of the displayed window.

       <window> (^Y) creates, destroys and moves between editing windows.  Z
         allows the screen to be broken up into up to 8 non-overlapping editing
         windows that each can contain different files.

         <window> moves to the next window to the right of or below the current
            window.

         <arg><window> splits the current window horizontally at the cursor.

         <arg><arg><window> splits the current window vertically at the cursor.

         <meta><window> merges the current window with one to the right or
            below.


                              Editing Switches and Flags

       Editing switches that take numerical values and their default values.

         bgcolor (0) gives the background color for the editing screen.  This
            is available only on the IBM PC version.



                                       - 16 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


         debug (0) controls display of macros while they are being executed.
            See the documentation on keystroke macros below.

         entab (1) controls the degree of tabification that Z performs when
            outputting a file.  entab:0 directs Z to output the file with no
            tabs.  entab:1 directs Z to attempt to entab all multiple spaces
            outside of quoted strings.  These strings are delimited either with
            quotes (") or apostrophes (').  entab:2 directs Z to maximally
            entab the line.

         errcolor (4) is the color used when displaying error messages on the
            screen.  This is available only on the IBM PC version.

         fgcolor (7) is the color used for foreground display of the editing
            windows.  This is available only on the IBM PC version.

         height (23) is the number of lines that Z uses in the editing window.
            This is useful when using a nonstandard display device:  EGA in 43-
            line mode on the IBM PC and Ambassador terminals are simple
            examples.

         hike (4) is the location on the screen of the cursor when the cursor
            is moved by editing functions.  Some of the cursor movement
            commands above move the cursor as opposed to scroll the cursor.
            Scrolling is controlled by the hscroll and vscroll parameters
            below.  For direct movement, hike is the position in the editing
            window where Z will place the cursor on the direct movement.

         hscroll (10) is the number of columns scrolled when the cursor is
            scrolled off of the editing window.

         infcolor (6) is the color used for information messages.  This is
            available only on the IBM PC version.

         rmargin (72) is the right margin column used in wordwrap mode.  Any
            space hit to the right of this margin causes a line break as does
            any character hit beyond the rmargin+4 position.  Wordwrap mode is
            set by the wordwrap switch below.

         stacolor (3) is the color used for the status line.  This is available
            only on the IBM PC version.

         tabstops (4) is the number of spaces between each logical tab stop on
            the editing screen.  Note that these tabstops are attached to the
            file and not to the window.

         tmpsav (20) is the number of files that Z remembers between editing
            sessions. When you exit Z, the specified number of files are saved
            in a temp file along with the position of the window and cursor
            within each.  Also saved is the layout of the windows you had
            created.






                                       - 17 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


         vscroll (7) is the number of lines scrolled when the cursor is
            scrolled off the editing window.  It is also the number of lines
            scrolled by the <plines> and <mlines> editing functions.

       Editing switches that are boolean in nature.  To set switch put switch:
       in TOOLS.INI, to reset switch put noswitch: in tools.ini, e.g. askexit:
       or noaskexit.

         askexit (off) causes Z to prompt for confirmation when you exit.

         askrtn (on) causes Z to prompt for confirmation when you return to
            after <push>

         autosave (on) causes Z to save the current file whenever you switch
            away from it. Some users prefer to issue a command to save the file
            rather than have Z "know" when to do it for them.

         case (off) causes Z to consider case to be significant for search and
            replace operations.

         enterinsmode (off) causes Z to start up in insert mode as opposed to
            overstrike mode.

         softcr (on) lets Z guess at proper indentation when the <newline> or
            <emacsnewl> editing functions are hit.

         trailspace (off) causes Z to remember trailing spaces in text.
            Normally, Z discards trailing spaces.

         wordwrap (off) causes Z to break lines of text on word boundaries when
            you edit them beyond the margin specified by rmargin.

       Editing switches that are textual in nature:

         backup (undel)is the method used for creating backup versions of
            edited files. The text that follows is one of the following:

         none    perform no backup operation.
         undel   delete the file so that the UNDEL command can retrieve it.
         bak     place the previous version in a version with the extension
         .bak.

         extmake (none)is used to associate a compiler and command line with a
            particular extension for use by the <compile> command.  The text
            that follows the switch is of the form:

                 extension command arguments

            where extension is the extension of the file to match, command is a
            command to execute and arguments are the parameters to be passed to
            the command.  There may be a %s in the arguments section  that is
            replaced with the name of the current file or with the selected
            text (see <compile>).  The special extension "text" is used to set
            the compiler command for when the user enters <arg>text<compile>.



                                       - 18 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


         markfile (none)is the name of the file Z searches when looking for a
            bookmark that is not in the in-memory set.

         readonly (none)is the command that will be invoked when z attempts to
            overwrite a readonly file.  The current file name will be appended
            to the command, e.g.

                 readonly: chmode -r


                                   Keystroke Macros

       The above set of editing functions are a fairly comprehensive set of
       functions that you can use in your day-to-day editing.  Often, however,
       you can come up with a set of operations that are commonly executed
       together.  Instead of entering each function separately, a tedious
       operation of the keyboard is not comfortably laid out, you can define
       new editing functions that are defined in terms of the previously
       defined set of functions.

       This is done in two steps.  First, a definition of the editing function
       in terms of the components needs to be done.  You would use the <assign>
       function or your TOOLS.INI file to create this definition.  Remember
       that editing the TOOLS.INI does not define the function, you must either
       exit Z or use the <initialize> function to process it.  Remember too,
       that if you use the <assign> function to define an editing function, you
       will lose this definition if you exit Z.  This operation defines the new
       editing function.

       The next step is to assign a keyboard sequence to this function, causing
       the function to be executed each time the specific keys are pressed.
       Again, this can be accomplished either by editing the TOOLS.INI or by
       using the <assign> editing function.

       Let's try two examples.  First, define and assign a function that will
       delete from the cursor through the end of the current or next word.
       Normally, this is accomplished by entering the following editing
       functions:

            <arg>          ; define the beginning of a sdelete argument
            <meta>
            <pword>        ; move to end of current/next word
            <sdelete>      ; delete from arg through the current cursor
            position
                           ; including all line breaks.

       Let's call this new function worddelete.  To define it in the TOOLS.INI
       file all we need to do is locate the [Z] tagged section and add the
       following line:

            worddelete:=arg meta pword sdelete

       Easy, eh?  To assign this to a keystroke sequence, say ALT-D on the IBM
       PC keyboard, we'd also enter the line:



                                       - 19 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


            worddelete:ALT-D

       Once we'd reinitialize the editor (either via the <initialize> command
       or by exiting Z and then starting it up again), each time we'd hit ALT-
       D, a word would disappear.

       To insert actual text into the file inside a macro all you need to do is
       enclose that text in quotes.  The second example below shows how.  Let's
       define a function that inserts a C-language "if" statement before the
       line with the cursor.  You'd do this normally by typing:

            <arg>
            2
            <linsert>      ; insert two blank lines
            <up>
            <newline>      ; let Z guess at the indentation
            "if () {"      ; place in the first part of the if <newline>
            "}"            ; close the consequent
            <up>
            <begline>      ; put the cursor back onto the if

       The TOOLS.INI entries for this are:

            insert-if:=arg "2" linsert up newline "if () {" newline "}" up
            begline
            insert-if:ALT-I

       All editing functions have return codes.  These values may be tested and
       acted upon by the following macro statements:

       :>label  defines a label that can be referenced in any of the below
         macro commands.

       =>label  is a direct transfer to the specified label.  If label  is
         omitted then the current macro is exited.

       ->label  directs transfer to the specified label  iff the previous
         editor function returned FALSE.  If label  is omitted then the current
         macro is exited.

       +>label  directs transfer to the specified label  iff the previous
         editor function returned TRUE.  If label  is omitted then the current
         macro is exited.














                                       - 20 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


       Below is a list of all the editor functions and their return conditions.

       Function       Condition for            TRUE Condition for FALSE
       arg            Always                   Never
       assign         Assignment was successful     Invalid arg or assignment
       backtab        Cursor moved             Cursor was at left margin
       begline        Cursor moved             Cursor did not move
       cancel         Always                   Never
       cdelete        Cursor moved             Cursor did not move
       compile        Exec of compiler succeeded    Bad arg, compiler not found
       down           Cursor moved             Cursor did not move
       emacscdel      Cursor moved             Cursor did not move
       emacsnewl      Always                   Never
       endline        Cursor moved             Cursor did not move
       exit           No return                No return
       home           Cursor moved             Cursor did not move
       information    Always                   Never
       initialize     Successful initialization     Bad arg
       insertmode     If insert mode was on    If insert mode was off
       ldelete        Successful line delete   Bad arg
       left           Cursor moved             Cursor did not move
       linsert        Successful line insert   Bad arg
       mark           Succ. definition or move Bad arg or mark not found
       meta           If meta was on           If meta was off
       mlines         Successful movement      Bad arg
       mpage          Successful movement      Bad arg
       mpara          Successful movement      Bad arg
       msearch        Found string             Bad arg or not found
       mword          Cursor moved             Cursor did not move
       newline        Always                   Never
       pbal           Balance was successful   Bad arg or not balanced
       pick           Successful pick          Bad arg
       plines         Successful movement      Bad arg
       ppage          Successful movement      Bad arg
       ppara          Successful movement      Bad arg
       psearch        Found string             Bad arg or not found
       push           Successful push          Bad arg or prog not found
       put            Always                   Never
       pword          Cursor moved             Cursor did not move
       qreplace       >= 1 replacement         Not found, invalid pattern
       quote          Always                   Never
       refresh        File was read in/deleted Canceled, bad arg
       replace        >=1 replacement          Not found, invalid pattern
       right          Cursor over text of line Cursor beyond end of line
       sdelete        Successful delete        Bad arg
       setfile        Not canceled, changed    Bad arg, canceled
       setwindow      Successful window change Bad arg
       sinsert        Successful insert        Bad arg
       tab            Cursor moved             Cursor did not move
       up             Cursor moved             Cursor did not move
       window         Successful split/join/move    Any error






                                       - 21 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


       
                                        Index

       
       commands
         <arg> (^X)................................................... 4
         <assign> (^^)................................................ 4
         <backtab> (SHIFT-TAB)........................................ 4
         <begline> (END).............................................. 4
         <cancel> (^C)................................................ 4
         <cdelete> (BACKSPACE or ^H).................................. 4
         <compile> (^U)............................................... 5
         <curdate>  (ALT-D)........................................... 5
         <curday>..................................................... 5
         <curfileext>................................................. 5
         <curfilenam>................................................. 5
         <curtime>  (ALT-T)........................................... 5
         <curuser>.................................................... 5
         <down> (DOWN arrow).......................................... 5
         <emacscdel> (CTRL-BACKSPACE)................................. 6
         <emacsnewl> (unassigned)..................................... 6
         <endline> (PGDN)............................................. 6
         <exit> (F9).................................................. 6
         <home> (HOME)................................................ 6
         <information> (F1)........................................... 6
         <initialize> (F2)............................................ 6
         <insertmode> (^N)............................................ 6
         <ldelete> (^F)............................................... 7
         <left> (LEFT arrow).......................................... 7
         <linsert> (^D)............................................... 7
         <mark> (^P).................................................. 7
         <meta> (ESC)................................................. 8
         <mlines> (^W)................................................ 8
         <mpage> (^Q)................................................. 8
         <mpara> (CTRL-PGUP).......................................... 8
         <msearch> (^E)............................................... 8
         <mword> (unassigned)........................................ 10
         <newline> (ENTER or ^M)..................................... 10
         <pbal> (^V)................................................. 10
         <pick> (^K)................................................. 10
         <plines> (^T)............................................... 11
         <ppage> (^L)................................................ 11
         <ppara> (CTRL-PGDN)......................................... 11
         <psearch> (^R).............................................. 11
         <push> (^Z)................................................. 12
         <put> (^G).................................................. 12
         <pword> (unassigned)........................................ 12
         <qreplace> (CTRL-ENTER or ^J)............................... 12
         <quote> (unassigned)........................................ 12
         <refresh> (F10)............................................. 12
         <replace> (^O).............................................. 13
         <restcur>................................................... 13
         <right> (RIGHT arrow)....................................... 13
         <savecurs>.................................................. 13



                                       - 22 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


         <sdelete> (^S).............................................. 14
         <setfile> (^B).............................................. 14
         <setwindow> (^])............................................ 14
         <sinsert> (^A).............................................. 15
         <tab> (TAB or ^I)........................................... 15
         <up> (UP arrow)............................................. 15
         <window> (^Y)............................................... 15
       switches
         boolean..................................................... 16
           askexit (off)............................................. 16
           askrtn (on)............................................... 16
           autosave (on)............................................. 16
           case (off)................................................ 17
           enterinsmode (off)........................................ 17
           softcr (on)............................................... 17
           trailspace (off).......................................... 17
           wordwrap (off)............................................ 17
         numerical................................................... 15
           bgcolor (0)............................................... 15
           debug (0)................................................. 15
           entab (1)................................................. 15
           errcolor (4).............................................. 16
           fgcolor (7)............................................... 16
           height (23)............................................... 16
           hike (4).................................................. 16
           hscroll (10).............................................. 16
           infcolor (6).............................................. 16
           rmargin (72).............................................. 16
           stacolor (3).............................................. 16
           tabstops (4).............................................. 16
           tmpsav (20)............................................... 16
           vscroll (7)............................................... 16
         textual..................................................... 17
           backup (undel)............................................ 17
           extmake (none)............................................ 17
           markfile (none)........................................... 17
           readonly (none)........................................... 17

       


















                                       - 23 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


                                   Revision History

       3 November 1986 version 7.43  Create unique file name for temp file.
       Code and data shrinkage by removing redundant routines.

       23 September 1986 version 7.42  Fix fScan from scanning one beyond EOF.
       Make pBal use setAllScan.  Add ability to enter arbitrary characters
       into <psearch>, <msearch>, <replace>, and <qreplace> pattern and
       replacement strings.  Preserve tabbing and spaces in non-edited lines.
       Fix shortname processing from the command line.  Fix problem with
       AdjustLines and deleting at top of file.

       19 August 1986 version 7.41  Fix undetected out-of-stack problem
       introduced in 7.35.

       19 August 1986 version 7.40  Fix bug in not highlighting search
       arguments when using default search from startup.

       18 August 1986 version 7.39  Fix bug introduced in 7.26 in
       <arg><arg><put>.  Optimize file loading code.

       8 August 1986 version 7.38  Fix bug introduced in 7.36 for reading
       TOOLS.INI.  Fix bug introduced in 7.37 for Z.$ temp file creation.

       4 August 1986 version 7.37  Fix problem in using TMP environment
       variable to locate <compile> temporary message file.

       1 August 1986 version 7.36  Allow path searching for temp files (Z.MSG,
       Z.$).  Allow path searching of <setfile> files.  Speed up
       initialization.

       7 July 1986 version 7.35  Shrink several VM routines.  Better out-of-
       space messages from VM.  Bug fix in textarg copying text from screen.
       Bug fix in macro redefinition while macros in progress.

       6 Jun 1986 version 7.34  Add macros savecur, restcur, curFileNam,
       curFileExt and editing switches readonly, askrtn, default ALT-T and ALT-
       D for curtime, curdate.

       13 May 1986 version 7.33  Recompiled using C 4.02.

       24 April 1986 version 7.32  Change <arg><arg><setfile> to remove dirty
       bit after successful save.

       10 April 1986 version 7.31  Fix bug that incorrectly updated the screen
       on line insert/delete at top of single window screen.  Add default
       assignments to <pword>, <mword>, and <curdate>.

       9 April 1986 version 7.30  When deleting/inserting lines, adjust other
       window instances to prevent rippling of displays in windows that are not
       affected by the deletion or insertion.

       8 April 1986 version 7.29  Fix problem in Z invocation with no arguments
       changing directory to the root.



                                       - 24 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


       8 April 1986 version 7.28  Renumbered for first public release.

       7 April 1986 version 7.27  Add /D switch to prevent user TOOLS.INI
       processing.  Add environment variable searching capability to all
       filename processing.

       3 April 1986 version 7.26  Add file put capability to <put>.  Add
       default time, date, and user macros.

       2 April 1986 version 7.25  Add autosave switch.  Remove savemeta switch.
       Fix bug that caused all new files to be NL-terminated.

       24 March 1986 version 7.24  Create dir search temp file on device
       specified by TMP directory.  Fixes problem of leaving temp file around
       in root.

       22 March 1986 version 7.23  Preserve LF-ness of files.

       14 March 1986 version 7.22  Make successful <compile> read first
       message.

       12 March 1986 version 7.21  Replace bakfile switch with backup.

       11 March 1986 version 7.20  Clear dialog line after clearing screen
       after <push>.

       11 March 1986 version 7.19  Reset video mode after prompt in <push>.

       24 Feb 1986 version 7.18  Change internal page hashing for less
       clustering of swap pages.  Add register optimization in redraw.

       23 Feb 1986 version 7.17  Hook ^Break to quickly detect <cancel> during
       searches and other time-consumptive operations.  Use INT 16h to read
       from the keyboard.  Remove erroneous message if no user TOOLS.INI is
       present.  Saving file under  another name changes the internal name too.

       18 Feb 1986 version 7.16  Restore/save video mode during <push>.  Allow
       assignment to <unassigned>.

       14 Feb 1986 version 7.15  Remove necessity for system-wide TOOLS.INI.
       Fix problem with DOS MAKE returning pseudo-files in errors.

       12 Feb 1986 version 7.14  With bakfile set and saving to a new file, Z
       was incorrectly reporting that it could not rename the new file to
       newfile.bak.

       30 Jan 1986 version 7.13  Cooking ^@ resulted in a NUL string.

       28 Jan 1986 version 7.12  Problems on XENIX with filenames with no name
       (like .profile).

       24 Jan 1986 version 7.11  Fix incorrect scrolling at top of screen and
       at left of screen.  Off-by-1 error.  Add message and prompt after
       successful <push>.



                                       - 25 -





       Z User's Guide
                                              Printed: November 5, 1986 11:52 AM


       15 Jan 1986 version 7.10  Fix incorrect buffer usage in <compile> code
       that prevented use of <arg><arg>streamarg<compile>.

       13 Jan 1986 version 7.9  If on EGA and height:41 then set EGA into 43-
       line mode.

       10 Jan 1986 version 7.8  Fix bug when final putlflush encounters full
       disk it did not report the error.

       10 Jan 1986 version 7.7  Fix bug in <macro> that prevented graphic
       characters at the end of a macro.

       7 Jan 1986 version 7.6  Adjust  return code semantics of <right> to
       allow for generation of a <fill> keystroke macro.  Added conditional
       description to document.

       6 Jan 1986 version 7.5  PC version no longer requires VT52.SYS.  Extmake
       to control <compile> commands.

       Please send all comments in machine readable form to tools.





































                                       - 26 -


