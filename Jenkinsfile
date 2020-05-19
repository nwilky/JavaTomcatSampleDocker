pipeline {
    agent any
    tools {
        maven 'LocalMaven'
    }


    stages {
        stage('Build Application') {
            steps {
                sh 'mvn -f pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Create Tomcat Docker Image'){
		
            steps {
                sh "pwd"
                sh "ls -a"
                sh "sudo -S 'picard' docker build -t tomcatsamplewebapp:${env.BUILD_ID} ."
            }
        }

    }
}