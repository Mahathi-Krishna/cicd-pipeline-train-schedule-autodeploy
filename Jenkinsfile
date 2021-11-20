pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = "mahathkrish/train-schedule"
    }
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage('Build & Push Docker Image') {
            steps {
                sh "docker build -f Dockerfile -t mahathkrish/train-schedule:'${env.BUILD_NUMBER}' ."
				sh 'docker login -u mahathkrish -p Krush@131295'
				sh "docker push mahathkrish/train-schedule:'${env.BUILD_NUMBER}'"				
            }
        }
    }
}
