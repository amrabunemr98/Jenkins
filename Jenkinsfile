pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS= credentials('docker-hub')
    }
    parameters {
        booleanParam(name:'Test-Jenkins', defaultValue: true, description:'this paramater help you to know project name')
        choice(name: 'namespace', choices:['Development','Testing','Production'], description: '' ) 
    }

    stages {
        stage('check') {
            steps {
                echo "checking your code"
                echo "${params.namespace}"
               
            }
        }
        stage('Build and Push Docker Image') {
            when {
                expression{
                    params.Test-Jenkins == true 
                }
            }
            steps {
                sh "docker build -t amrabunemr98/sprintsjenkins:${BUILD_TAG} ."
                sh "docker push amrabunemr98/sprintsjenkins:${BUILD_TAG}"
                echo "Push Docker Image is successed" 
            }
        }
        
        stage('deployment') {  
            steps {
                echo "your code is deployed right now"
                echo "this build number $BUILD_NUMBER"
            }
        }    
    }

}
