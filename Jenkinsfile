pipeline {
    agent any
    tools {
        maven "M3"

    }
        stages {
            stage ('checkout') {
                steps {
                  checkout scmGit(
                  branches: [[name: '*/feature']], extensions: [],
                  userRemoteConfigs: [[url: 'https://github.com/sarimheyat/simple-java-maven-app.git']])

                }
            }
            stage ('Build') {
                steps {
                    sh 'mvn -f pom.xml clean install -DskipTests'
                }
            }
            stage ('Test') {
                steps {
                    sh 'mvn clean test -T5 -B -U'
                }
            }
            stage ('shell command') {
                steps {
                    catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                    sh 'systemctl status docker'
                    }
                }
            }
        }
        /*** workspace clean up*/
    post {
        always {
            cleanWs()
        }
    }

}
