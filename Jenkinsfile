pipeline {
    agent { 
        node {
            label 'docker-agent-python'
            }
      }
    triggers {
        pollSCM '*/5 * * * *'
    }
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                python3 app.py
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "Delivery step to be worked upon"
                '''
            }
        }
    }
post {
    failure {
        mail to: 'prabinpaudel43@gmail.com',
             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL}"
    }

success {
	mail to: 'prabinpaudel43@gmail.com', subject:"Build completed: ${currentBuild.fullDisplayName}",
             body: "You have a successfully built pull request pending."
    } 
}

}