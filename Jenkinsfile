pipeline {
    agent any
	
	environment {
        DOCKER_IMAGE = 'alpine:3.3'
        // DOCKER_IMAGE = 'alpine:latest'
    }

    stages {
        stage('Upload to AWS') {
            steps {
                sh 'echo "Hello World"'
				sh '''
				echo "Multiline shell steps works too"
				ls -lah
				'''
            }
        }        
        stage('Lint HTML') {
            steps {
                echo 'Verifying HTML Syntax....'
				sh 'tidy -q -e *.html'
            }
        }
		stage('Upload to S3 Bucket') {
            steps {
				withAWS(region:'us-west-2',credentials:'aws-static') {
					sh 'echo "Uploading content with AWS credentials"'
					s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'iftaa-jenkins-bucket')
				}
            }
        }		
    }
}
