pipeline {
    agent any
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
				sh "sudo usermod -a -G docker $USER"
                sh "docker build -f Dockerfile -t tomcatsamplewebapp:${env.BUILD_ID} ."
            }
        }

    }
}