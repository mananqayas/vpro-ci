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
        SONERSERVER='sonarserver'
        SONERSCANNER='sonarscanner'
    }
    stages {

        stage ('Build')

        {

            steps {



                sh 'mvn -s settings.xml -DskipTests install'


            }

            post {

                success {

                    echo 'Now Archiving ...'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }

        }

        stage ('Test'){

            steps {



sh 'mvn -s settings.xml  test'
            }
        }

        stage ('Checkstyle analysis'){
            steps {



            sh 'mvn -s settings.xml  checkstyle:checkstyle'
            }
        }
               stage('Sonar Analysis') {
            environment {
                scannerHome = tool "${SONARSCANNER}"
            }
            steps {
               withSonarQubeEnv("${SONARSERVER}") {
                   sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                   -Dsonar.projectName=vprofile \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
              }
            }
        }
    }
}
