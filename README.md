# Project 1d: ROT13 Cipher

You are to implement a very simple encoder and decoder using the classic [ROT13 Cipher](http://www.crypto-it.net/eng/simple/rot13.html). Don't worry, it looks WAY worse than it actually is.

The script, `rot_encrypt.py`, should: 

1. Open the file specified as the first argument to the script (see below)
2. Read the file one line at a time (i.e., for line in file)
3. For each line, the basic alogrithm is as follows:
    - strip() any extra spaces or newlines from the beginning or end of the line
    - create an empty string called `enc_string`
    - now you want to iterate over each CHARACTER in the line. For each:
        - If the character is NOT a character in [A-Za-z] (use isalpha()), just append it to your `enc_string` string and go on to the next character
        - Otherwise use the `ord()` funciton to retrieve the ordinal value of the character and store it in a `char_num` variable (will be between 65 for 'A' and 90 for 'Z' or between 97 for 'a' and 122 for 'z')
        - Subtract from 65 `char_num` if it is an upper case character or 97 from char_num if it is a lower case character...this will give you a value between 0 and 25
        - Add 13 to `char_num` (value will be between 13 and 38)
        - Get the remainder of `char_num` when dividing by 26 (i.e., `char_num = char_num % 26`--character values of 13 to 25 stay the same, but values of 26 to 38 become 0 to 12 because that's the remainder when dividing by 26)
        - Add 65 or 97 back to `char_num` depending on whether it was a capital or lower case character
        - Convert `char_num` back to a character using the `chr()` function and concatenate that character to the end of `enc_string`
        - The end result is that 'A' becomes 'N', 'B' becomes 'O', 'C' becomes 'P' and so on
    - RETURN `enc_string`
4. Print each encrypted line to the screen

Most of step 3 is just performing some fifth-grade math to make it easy to shift each character 13 places to the right. Do your best to REALLY understand what that is doing. That kind of numerical manipulation of characters can be VERY handy, especially in the world of cyber security. 

This particular cipher is pretty neat in that the same cipher both ENcodes and DEcodes the text. In fact, if you do your job right, you should be able to run your script agains the `sample_rot_testmsg.txt` and you'll get a the original message back (well, all upper case). Of course, it's perhaps the least secure cipher imaginable, so, you know, don't ever, Ever, EVER actually use it for anything important.

## HINTS 

1. The "arguments" to a python program are in the sys.argv list. The first element in the list is the name of the script and the rest are any additional words (arguments) added to the end. [See here for explanation](https://www.tutorialspoint.com/python/python_command_line_arguments.htm). The code needed may look as follows:
```
import sys

filename = sys.argv[1]
```

## REQUIRED IMPLEMENTATION NOTES 

1. You MUST abstract your most useful logic by creating a function named `encrypt_string` that takes string as a parameter and returns the encrypted string. This function should be "called" as your step 3 above, which will make the main script much cleaner. In other words, the main part of your script should open the file, iterate over each line in the file, and the following function MUST be defined in your script and called to encrypt each line:

``` 
        def encrypt_string(string): 
            ... ENCRYPT THE STRING ...
            return enc_string
``` 
2. You MUST edit `testmsg.txt` and add a line with __your__ name in it; perhaps something like "Paul York was here". JUST edit and save the file using VS code or another text editor. No Python code required here.

3. You MUST run your script against the edited version of `testmsg.txt` and redirect the output to `rot_testmsg.txt`. In other words, you should run `python rot_encrypt.py testmsg.txt > rot_testmsg.txt`. Include this file in your final submission. __DO NOT WRITE TO A FILE INSIDE OF YOUR SCRIPT. ONLY READ AND PRINT. WRITING OCCURS HERE BY REDIRECTING OUTPUT.__

Note: If you do output redirection in Windows Powershell (the default shell for VS Code), it writes the file using Unicode, which can cause issues. Use a standard Command Prompt (cmd.exe) if running this in Windows. Should not have any issues on Mac or Linux (and thus Mimir).

When done, be sure to test the heck out of this and then submit the __project1 directory__ in Mimir.

## OPTIONAL CHALLENGES 

1. Create a second version of the script, encrypt_string2.py. This version should import the rot13 function from encrypt (`from rot_encrypt import encrypt_string`). Instead of asking for a file name and reading the text from the file, read in the text line-by-line from `sys.stdin`. This should allow you to run it interactively AND to pipe in text from another command (e.g., `type testmsg.txt | python encrypt2.py`). Even cooler here, you can "double-pipe" the output and get the original back (e.g., `type testmsg.txt | python encrypt_string2.py | python encrypt_string2.py`)

2. Swap lower and upper case characters during the encode and decode process. You know, 'cause it's sooooo much harder to rEAD tEXT wRITTEN lIKE tHIS.

3. Make the shifting "variable". In other words, ask how many characters to shift (13 is "default", but can supply any number).
