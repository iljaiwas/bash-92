#Update:

There is an official GNU patch for the OS version of batch now. Instructions on how to apply can be found in this [stack exchange post](http://apple.stackexchange.com/questions/146849/how-do-i-recompile-bash-to-avoid-the-remote-exploit-cve-2014-6271-and-cve-2014-7).

This is its gist:

<pre>
$ mkdir bash-fix
$ cd bash-fix
$ curl https://opensource.apple.com/tarballs/bash/bash-92.tar.gz | tar zxf -
$ cd bash-92/bash-3.2
$ curl https://ftp.gnu.org/pub/gnu/bash/bash-3.2-patches/bash32-052 | patch -p0    
$ cd ..
$ xcodebuild
$ sudo cp /bin/bash /bin/bash.old
$ sudo cp /bin/sh /bin/sh.old
$ build/Release/bash --version # GNU bash, version 3.2.52(1)-release
$ build/Release/sh --version   # GNU bash, version 3.2.52(1)-release
$ sudo cp build/Release/bash /bin
$ sudo cp build/Release/sh /bin
</pre>


#My Original version:
Since there is no official patch from Apple yet for the recently published [shell vulnerability](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6271), here is a version of the bash that ships with OS X 10.8.x and 10.9.x, which turns off the bash feature responsible for the exploit.

The source for this version of bash is taken from Apple's [open source website](http://opensource.apple.com/source/bash/bash-92/).

Check if your Mac is vulnerable:

`test="() { echo Hello; }; echo vulnerable" bash -c ""`

If you see vulnerable printed out, you are not safe yet.

How to patch your Mac:

* Clone this repository
* Build the bash target in Xcode 5.1.1 on OS X 10.9.5
* backup your original bash in case something goes wrong: `sudo cp /bin/bash /bin/bash.orig`
* install the shell Xcode just built:` sudo cp <wherever xcode put me>/bash /bin bash`

For me the patched bash worked on OS X 10.8.5 and 10.9.5.

If you check with the line from above again, you should see this:

`bash: error importing function definition for test`