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
		sh "sudo docker build -f Dockerfile -t mahathkrish/train-schedule:'${env.BUILD_NUMBER}' ."
		sh 'sudo docker login -u mahathkrish -p Krush@131295'
		sh "sudo docker push mahathkrish/train-schedule:'${env.BUILD_NUMBER}'"				
            }
        }
	stage('DeployToProduction') {
            steps {
		sh 'chmod 777 train-schedule-kube.yml'
		sh 'kubectl create -f train-schedule-kube.yml'
            }
        }
    }
}
