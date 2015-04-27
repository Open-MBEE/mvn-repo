mvn-repo
========

Repository for hosting artifacts (e.g., amps, zips, etc.)

Can use github as a maven repository. Instructions at http://stackoverflow.com/questions/14013644/hosting-a-maven-repository-on-github

Installation instructions
=========================

Installing AMPs

# Uninstall any existing amps
    cd $TOMCAT/webapps
    java -jar $ALFRESCO/bin/alfresco-mmt.jar uninstall mms-repo alfresco.war
    java -jar $ALFRESCO/bin/alfresco-mmt.jar uninstall mms-share share.war
# Install the amps
    java -jar $ALFRESCO/bin/alfresco-mmt.jar install $PATH_TO_AMP/mms-repo.amp $TOMCAT/alfresco.war -force
    java -jar $ALFRESCO/bin/alfresco-mmt.jar install $PATH_TO_AMP/mms-share.amp $TOMCAT/share.war -force
# Explode the alfresco.war in the $TOMCAT/webapps directory
    rm -rf alfresco
    mkdir alfresco
    cd alfresco
    jar xvf ../alfresco.war
# Unzip EVM into alfresco directory, move to the correct place, and update the permissions
    unzip evm.zip .
    mv build mmsapp
    cd $TOMCAT/webapps
    chown -R tomcat:tomcat webapps
# Note you will probably need to update the permissions on all the directories, files, touched
