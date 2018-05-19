node {
    stage ('scm checkout') {
    checkout([$class: 'GitSCM',
    branches: [[name: '*/master']],
    doGenerateSubmoduleConfigurations: false,
    extensions: [], submoduleCfg: [],
    userRemoteConfigs: [[url: 'https://github.com/pawarsachin84/helloworldweb.git']]])
    }

    stage ('Appbuild') {
    sh 'mvn -f pom.xml clean package'
    }
    
    stage ('deployment') {
    sh '''cp target/*.war /opt/apache-tomcat-8.5.31/webapps/
    sudo sh /opt/apache-tomcat-8.5.31/bin/shutdown.sh
    sudo sh /opt/apache-tomcat-8.5.31/bin/startup.sh'''
    }
    stage ('archive Artifacts') {
    archiveArtifacts 'target/*.war'
    }
}
