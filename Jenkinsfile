pipeline {
    
    agent any
    
    environment {
        MAVEN_PATH="/usr/share/maven/bin:${MAVEN_PATH}"
       // BRANCH_NAME="${env.BRANCH_NAME}"
    }
    
    stages {
        
        stage ('checkout') {
            steps {
                git branch:'env.BRANCH_NAME', url: 'https://github.com/sarimheyat/simple-java-maven-app.git'
            }
        }

    
    stage ('Build') {
        steps {
            
            sh 'mvn clean install -DskipTests -B -U -T 5'
        }
    }
    
    stage ('Test') {
        steps {
            sh 'mvn clean test -T 10'
        }
    }
    
    
    stage ('Deploy playbook') {
        steps {
            sh 'sudo ansible-playbook /etc/ansible/playbook/playbook1.yaml'
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
