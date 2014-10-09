perl-acpi-fanspeed
==================

Control your ACPI system fan curve in unix environments by writing to your Embedded Controller registers.

USE THIS AT YOUR OWN RISK! I TAKE NO RESPONSIBILIY FOR USE OR MISUSE OF THE FILES IN THIS PROJECT

This is a script I found online here: http://aceracpi.googlecode.com/svn/trunk/acer_ec/acer_ec.pl

The original purpose is defined here: https://code.google.com/p/aceracpi/wiki/EmbeddedController

The RW Everything scripts I found for my MSI GT60 2OC: (will find link)


My reason for modifying the script was to allow me to change my fan speed curve easily and efficiently. On Windows, I found the need to use the program RW Everything in order to accomplish this task. On unix environments I couldn't find any useful responses for how to do this, so I came up with this solution (again, based off the script I borrowed).

*IMPORTANT*
Most of the functions in the original script I have ignored and DO NOT RECOMMEND using unless you have one of the acer machines mentioned in the links above. Please also note that the specific registers for each system are different, so this script SHOULD NOT BE USED OUT OF THE BOX WITHOUT MODIFICATION. My modifcations to this script are specific to my MSI GT60 2OC laptop.

===%%===

That aside, I will now do my best to document what the portions I am using do, and how to modify them to meet the needs of your own machine. I am not all that great at writing documentation for this type of thing, so feel free to ask me questions.

To start off, really the only commands that are of absolute importance are "regs" and "writetemp", which are invoked like so:

<code>sudo ./acer_ec.pl regs</code>

<code>sudo ./acer_ec.pl writetemps [reg] [val]</code>

Most of the other commands are merely supplemental to these. regs will show you the contents of the EC registers and writetemps will allow you to write to a specific register (decimal values only). There is also a writetempshex command, used the same way, that will allow you to use hex values instead of decimal.

Now for the stuff that I have written to speed up the process. Again, please keep in mind these are specific to my laptop, but can be easily tweaked to your own system provided that you know what registers contain the values you intend to modify. I will start off with the myregs command:

<code>sudo ./acer_ec.pl myregs</code>

This was built with my specific laptop in mind, as well as the fact that the output was tailored to look like the RW Everything xml document (3rd link above) for easy comparison. To apply this to your own known values should be fairly simple if you know anything about any type of language. In the perl script, the function print_myregs2 is the one to modify. Compare this function to the xml macro output and you should be able to piece together what it does. Make sure the offsets are for your machine. *NOTE* this function only prints registers, so SHOULD NOT cause any harm. You may want to use it to try and find which ranges you need if you do not already know.


Next up is the setprofile command:
<code>sudo ./acer_ec.pl setprofile [profile]</code>

This again is specific to my own laptop and was coded to the .rw output files of the xml macro. Note that these are RW Everything command files, so if you already have some you use in Windows, then they should work here too. All this function does is parse the .rw file specified and apply each command one by one. It also gives you a before and after printout using the same print_myregs2 function above. This means they may not match up correctly if you have not modified the myregs functionality. The perl function for this is run_profile.
