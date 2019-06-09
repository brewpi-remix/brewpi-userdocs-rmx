About Security
==============
My instructions will tell you to copy and paste a command into your terminal window.  Despite me telling you to do that, I am now going to tell you how *unsafe* that is.  Many people browse the Internet, find the command they need, and blindly paste it into their terminal window.  This one is (potentially) **dangerous** from a non-trusted source:

.. code-block:: console

    curl -L install.brewpiremix.com | sudo bash

Here's how to decode it:  In this case I've provided an easy to remember Internet address `install.brewpiremix.com <install.brewpiremix.com>`_ on my website.  That's not actually where it goes however because on that website I have it redirecting to the `real script <https://raw.githubusercontent.com/lbussy/brewpi-tools-rmx/master/bootstrap.sh>`_ on GitHub. That script is then piped (via the `|` character) through the command `sudo bash`.  When you use `sudo` it will run the command which *follows* with `root` privileges.  So, you basically found someone on the Internet telling you to run their code as root, without even knowing what it all does.  Seems scary now, doesn't it?

Despite the inherent risk, installing an application as root is often necessary since many applications have to make global changes to your system.  In this case I am helping you by installing various helper packages for BrewPi, setting up system services like the Apache web server which allows you to connect to BrewPi, creates the actual user `brewpi` under which the scripts run, and some other necessary housekeeping.

**This is how bad things happen.**

Even if you think you *completely* understand the command you are reading and copying, there is still an opportunity for a specially crafted web page to make the command look like one thing, but be a completely different command when you paste it.  That would be **A Bad Thing™.**  For an example, see `this page which describes this copy/paste vulnerability <https://www.brewpiremix.com/copy-paste-and-you/>`_.

The lesson to be learned from this is if you are going to copy/paste a command from *any* source, always use an interim paste into a text editor like Notepad or type it in manually to make sure **A Bad Thing™** doesn't happen to you.

Wait.

Now you don't know if you should trust the setup command I provided?  I'm shedding a happy tear.  Security and the Internet is a rabbit hole filled with (justifiable) paranoia and bad actors.  Your choices here however are:

1. Trust me and run it, or;
2. Examine `that script <https://github.com/lbussy/brewpi-tools-rmx/blob/master/bootstrap.sh>`_ carefully and make sure it does nothing bad.  Then, since the first one executes as root you need to follow that to the `next one <https://github.com/lbussy/brewpi-tools-rmx/blob/master/install.sh>`_ because it inherits that security construct from the first.

Ultimately you can drive yourself crazy when you realize the implications, or just accept that whenever you install free code from the Internet you take your chances.  This is the case with any software, not just BrewPi.

Now, newly armed with facts, you can head back to :doc:`the automated install instructions <./index>` to get back on track.
