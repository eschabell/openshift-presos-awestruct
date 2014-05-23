How to run Awestruct Presentation Hosting on OpenShift
======================================================

This will give you an empty ruby instance on OpenShift for hosting your presentations on an Awestruct site.

Installation
------------

Create OpenShift application

    rhc app create -a presos -t ruby-1.9 --from-code=https://github.com/eschabell/openshift-presos-awestruct.git

or

    rhc app create -a presos -t ruby-1.9
    
    cd presos
    
    git remote add upstream -m master git://github.com/eschabell/openshift-presos-awestruct.git

    git pull -s recursive -X theirs upstream master

    git push
    
now build your presentation using Awestruct. Once done, copy the _site directory to your OpenShift instance.

    cp -rv  $project/_site presos/lib

To deploy to OpenShift just commit and push

    git add presos/lib/*

    git co -a

    git push origin master

If you add an index.html file with the links to each presentation you have installed on the site, then you can find them here

    http://presos-$namespace.rhcloud.com

What is this project doing?
---------------------------

* Install awestruct if not available (ruby gems)
* Update awestruct when already available (ruby gems)
* Install or updage needed deps (ruby gems)
* Generate the site and deploy it

Releases
--------

- v0.3 - moved to ruby cartridge, now building site from lib dir each push.

- v0.2 - build script adjusted to add missing deps in new OpenShift cartridge setup.

- v0.1 - initial setup.
