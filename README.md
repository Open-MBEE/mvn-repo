mvn-repo
========

Repository for hosting artifacts (e.g., amps, zips, etc.)

Can use github as a maven repository. Instructions at http://stackoverflow.com/questions/14013644/hosting-a-maven-repository-on-github

Preinstall Instructions
=======================
Make sure all your system paths, Java, Alfresco, and Tomcat set. These might vary depending on where you installed them.
To do so:

# Java path    

    sudo vi /etc/profile.d/java.sh

Copy paste

    export JAVA_HOME=/lib/jvm/jre-1.7.0-openjdk
    export PATH=$PATH:$JAVA_HOME

Save


# Alfresco path    
    
    sudo vi /etc/profile.d/alfresco.sh
    
Copy paste

    export ALFRESCO=/opt/alfresco{Version}
    export PATH=$PATH:$ALFRESCO
    
Save

# Tomcat path

    sudo vi /etc/profile.d/tomcat.sh

Copy Paste

    export TOMCAT=/opt/alfresco{VERSION}/tomcat
    export PATH:$PATH:$TOMCAT

# Add Path to Amps
    
    cd ~/git
    git clone https://github.com/open-mbee/mvn-repo

Add amps to path

    sudo vi /etc/profile.d/path_to_amp.sh

Copy paste

    export PATH_TO_AMP=~/git/mvn-repo
    export PATH=$PATH:$PATH_TO_AMP

Save
    
close terminal
* Optional

    cd ~/git/mvn-repo
    
    mv mms-repo-#####...amp mms-repo.amp
    
    mv mms-share-#####...amp mms-share.amp


* NOTE: That if you get a 'module.properties' error when installing the amps, it is most likely the version of either the repo or share amp. Remove the version that is failing and try the other version of the amp file.


Installation instructions
=========================

Installing AMPs

# Uninstall any existing amps
    cd $TOMCAT/webapps
    java -jar $ALFRESCO/bin/alfresco-mmt.jar uninstall mms-repo alfresco.war
    java -jar $ALFRESCO/bin/alfresco-mmt.jar uninstall mms-share share.war
# Install the amps
    cd $TOMCAT/webapps
    java -jar $ALFRESCO/bin/alfresco-mmt.jar install $PATH_TO_AMP/mms-repo.amp $TOMCAT/webapps/alfresco.war -force
    java -jar $ALFRESCO/bin/alfresco-mmt.jar install $PATH_TO_AMP/mms-share.amp $TOMCAT/webapps/share.war -force
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
