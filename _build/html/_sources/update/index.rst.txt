Updating BrewPi
===============
The script will stop the BrewPi script when it executes.  To run the update script, use the following command:

.. code-block:: console

    sudo /home/brewpi/doUpdate.sh

The script will actually download the update script currently on the GitHub abd re-execute that in order to take advantage of any updates to the script itself.

If merging the updates fails, the script will ask you to stash your local changes. This commits your changes to the git stash and bring your repository back to its original state. You can get your changes back with 'git stash pop', but be warned that your changes could be incompatible with the latest updates.

Scripts After Update
---------------------------------
After updating, the updater calls several other scripts from the Scripts area.  These are:

==========================  =====
Script                      Function
==========================  =====
doDepends.sh                Checks for updates to the following:
                             - apt packages
                             - pip packages
                            Removes the following if they are installed:
                             - PHP5 files
                             - nginx files
doCleanup.sh                Removes:
                             - \*.pyc files
                             - Empty directories
doDaemon.sh                 Install and/or update the daemon unit files which run BrewPi and optionally the WiFi Checker
doPerms.sh                  Sets permissions on the following:
                             - Script directories
                             - Web directories
                             - Bluetooth stack
==========================  =====

Updating Multi-Chamber
----------------------
You will need to run the `doUpdate.sh` script from each chamber's instance in order to upgrade all of them.
