About My Experiences Creating DEB Packages Plus Ubuntu's PPA
============================================================

As a noob in the *deb* packaging process, it was a bit painful to get the whole stuff
in place. After much reading and headaches, I finally made it. Here my conclusions:

- As first and super important first step, do all defined here <http://packaging.ubuntu.com/html/getting-set-up.html>.
There's a lot of things to set up, but it's the mandatory first step.

- Ubuntu documentation on how to make things work \(<http://packaging.ubuntu.com/html/packaging-new-software.html>\)
is good, but it doesn't cover all aspects, as installation scripts or pre/post
scripts. It just give some general approaches or links as last resource, that turned
out to be critical in my experience.
Changing folders commands are not reliable as explained there. Some commands must be
run at different folder levels.
And finally, what did the trick was to add **install** file. Without it package
was created in an incomplete fashion.

Now, this is **important**, to include any file added, it is necessary to perform a `bzr add`.
That's not mentioned in docs, but without that, files like **install**, **postinst** and
**prerm** weren't included.

**Important** to mention too, it's better to perform all the build process inside a
sub folder, as the whole thing creates packages and folders in a place next to where
the main code is located, not good, at all.

- If you, as me, are not a bzr user, just add a .gitignore file to not track info
generated in *.bzr* folder. You'll still see *.git* folder inside PPA's code link,
but that's fine and desirable.

- There's no need to remove *.git* folder while packing, as the system gets rid
of removing it.

- Not really sure if this is different under the Ubuntu way of doing things, but while
doing my checks, I found `dch -i` is a MUST in order to generate new packages, as
the changes go hand in hand with changelog.

- I got some ideas from this other places too, just to build a more complete understading
of things:

    * <http://askubuntu.com/questions/71199/manually-created-deb-how-do-i-upload-to-a-ppa>
    * <https://developer.ubuntu.com/en/publish/other-forms-of-submitting-apps/ppa/>
    * <http://askubuntu.com/questions/279686/how-to-package-a-simple-bash-script>
    * <http://askubuntu.com/questions/27715/create-a-deb-package-from-scripts-or-binaries/27731#27731>
    * <http://askubuntu.com/questions/71510/how-do-i-create-a-ppa>
    * <https://www.leaseweb.com/labs/2013/06/creating-custom-debian-packages/>

Things still not clear are differences between **DEBIAN** and **debian** folders.
There is documentation either refering to one or the other. In the end, lowercase
version seemed to do the trick in Ubuntu PPA relationship.

