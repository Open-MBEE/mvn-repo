mvn-repo
========

Repository for hosting artifacts (e.g., amps, zips, etc.)

Can use github as a maven repository. Instructions at http://stackoverflow.com/questions/14013644/hosting-a-maven-repository-on-github

Installation instructions
=========================

Installing AMPs

# Uninstall any existing amps
    java -jar alfresco-mmt.jar uninstall mms-repo/mms-share
# Install the amps
    java -jar alfresco-mmt.jar install mms-repo.amp alfresco.war -force
# Explode the alfresco.war in the webapps director
    mkdir alfresco
    cd alfresco
    jar xvf ../alfresco.war
# Unzip EVM into alfresco directory, move to the correct place, and update the permissions
    unzip evm.zip .
    mv build mmsapp
    chown -R alfresco:alfresco mmsapp
# Note you will probably need to update the permissions on all the directories, files, touched
