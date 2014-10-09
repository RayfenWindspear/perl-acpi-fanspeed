perl-acpi-fanspeed
==================

Control your ACPI system fan curve in unix environments by writing to your Embedded Controller registers.

This is a script I found online here: http://aceracpi.googlecode.com/svn/trunk/acer_ec/acer_ec.pl

The original purpose is defined here: https://code.google.com/p/aceracpi/wiki/EmbeddedController



My reason for modifying the script was to allow me to change my fan speed curve easily and efficiently. On Windows, I found the need to use the program RW Everything in order to accomplish this task. On unix environments I couldn't find any useful responses for how to do this, so I came up with this solution (again, based off the script I borrowed).

*IMPORTANT*
Most of the functions in the original script I have ignored and DO NOT RECOMMEND using unless you have one of the acer machines mentioned in the links above. Please also note that the specific registers for each system are different, so this script SHOULD NOT BE USED OUT OF THE BOX WITHOUT MODIFICATION.

That aside, I will now do my best to document what the portions I am using do, and how to modify them to meet the needs of your own machine.

