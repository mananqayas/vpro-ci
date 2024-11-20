pipeline {

    agent any
        tools {

            maven "MAVEN3"
            jdk "OracleJDK8"
        }


    environment {


        SNAP_REPO='vprofile-snapshot'
        NEXUS_USER='admin'
        NEXUS_PASS='Mjunhybgt123'
        RELEASE_REPO='vprofile-release'
        CENTRAL_REPO='vpro-maven-central'
        NEXUS_GRP_REPO='vprofile-maven-group'
        NEXUS_LOGIN='nexuslogin'
        NEXUSIP='172.31.35.26'
        NEXUSPORT='8081'
    }
    stages {

        stage ('Build')

        {

            steps {


                sh 'mvn -s settings.xml -DskipTests install'


            }

        }
    }
}
