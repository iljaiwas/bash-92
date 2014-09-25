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