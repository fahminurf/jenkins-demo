pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo "Stage Build "'
                sh 'chmod +x script.sh'
                sh './script.sh'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Stage Test "'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "Stage Deploy  (simulasi)"'
            }
        }
    }
}
