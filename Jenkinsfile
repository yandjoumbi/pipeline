pipeline{

	
        agent {label 'agent-01'}

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
		// AWS_ACCOUNT_ID = "597647611698"
        // AWS_DEFAULT_REGION = "us-east-1"
		// IMAGE_REPO_NAME= "yandjoumbi"
		// IMAGE_TAG = "latest" 
		// REPOSITORY_URI = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}" 
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t yandjoumbi/yann-dj:0.0.4 .'
				//dockerImage = docker.build "yandjoumbi:latest"
			}
		}

        
		stage('Login') {
         	withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
				steps {
					//sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
					//sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 597647611698.dkr.ecr.us-east-1.amazonaws.com'	
					//sh 'aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/yandjoumbi'
					sh 'docker login -u yandjoumbi -p ${dockerhub}'	    
				}
		 	}
		}

		stage('Push') {

			steps {
				sh 'docker push yandjoumbi/yann-dj:0.0.4'
				// sh 'docker tag yandjoumbi:latest 597647611698.dkr.ecr.us-east-1.amazonaws.com/yandjoumbi:latest'
				// sh 'docker push 597647611698.dkr.ecr.us-east-1.amazonaws.com/yandjoumbi:latest'

			}
		}
	
	
		post {
			always {
				sh 'docker logout'
			}
		}	
	}
}

