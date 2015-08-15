# SHC: Shell script to Binary converter

### Purpose:

        A generic shell script compiler. Shc takes a script, which is
        specified on the command line and produces C source code. The
        generated source code is then compiled and linked to produce a
        stripped binary executable. Use with care.

## DESCRIPTION
shc creates a stripped binary executable version of the script specified with -f on the command line.

The binary version will get a .x extension appended and will usually be a bit larger in size than the original ascii code. Generated C source code is saved in a file with the extension .x.c

If you supply an expiration date with the -e option the compiled binary will refuse to run after the date specified. The message "Please contact your provider" will be displayed instead. This message can be changed with the -m option.

You can compile any kind of shell script, but you need to supply valid -i, -x and -l options.

The compiled binary will still be dependent on the shell specified in the first line of the shell code (i.e. #!/bin/sh), thus shc does not create completely independent binaries.

shc itself is not a compiler such as cc, it rather encodes and encrypts a shell script and generates C source code with the added expiration capability. It then uses the system compiler to compile a stripped binary which behaves exactly like the original script. Upon execution, the compiled binary will decrypt and execute the code with the shell -c option. Unfortunatelly, it will not give you any speed improvement as a real C program would.

shc's main purpose is to protect your shell scripts from modification or inspection. You can use it if you wish to distribute your scripts but don't want them to be easily readable by other people.  

### Version 

3.8.9

### Changelog

See CHANGES file

## How to use

#### Install Required Packages

Install required packages for SHC compiler.
For Debian/Ubuntu

'''
$ apt-get install libc6-dev 
'''

For RHEL/CentOS

'''
$ yum install glibc-devel
'''

### Building

Download the latest source code of SHC compiler
Now compile the SHC source code on your system and install it using following command.

'''
$ cd shc-3.8.9
$ make 
$ make install
'''

### Create binary

Use following command to create binary file of your script.sh

'''
$ shc -T -f script.sh
'''

## OPTIONS

The command line options are:

-e date
    Expiration date in dd/mm/yyyy format [none] 
-m message
    message to display upon expiration ["Please contact your provider"] 
-f script_name
    File name of the script to compile 
-i inline_option
    Inline option for the shell interpreter i.e: -e 
-x comand
    eXec command, as a printf format i.e: exec(\\'%s\\',@ARGV); 
-l last_option
    Last shell option i.e: -- 
-r
    Relax security. Make a redistributable binary which executes on different systems running the same operating system. 
-v
    Verbose compilation 
-D
    Switch on debug exec calls 
-T
    Allow binary to be traceable (using strace, ptrace, truss, etc.) 
-C
    Display license and exit 
-A
    Display abstract and exit 
-h
    Display help and exit 


#### Testing

        Caveat emptor: see Copyright

        The results look fine to me, but I havn't used this in anger, but
        the author has used shc for his work widely over SunOS, Solaris and
        Linux, and done some testing on Irix and HPUX.
        We tested it on a few SMALL ksh scripts - big tasks should probably
        be written in C in the first place (see _SC_ARG_MAX below)!


#### Bugs

        The one (and I hope the only) limitation using shc is the
        _SC_ARG_MAX system configuration parameter.

        It limits the maximum length of the arguments to the exec function,
        limiting the maximum length of the runnable script of shc.

        !! - CHECK YOUR RESULTS CAREFULLY BEFORE USING - !!

## Credits

Author:  Francisco Rosales Garcia
http://www.datsi.fi.upm.es/~frosal

## LICENSE

GPL v2