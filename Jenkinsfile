pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building Maven Apps'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing Maven Apps'
            }
        }
         stage('Deploy') {
            steps {
                echo 'Deploying Maven Apps'
            }
        }
    }

    
    post {
        always {
            echo "always say hello to you"
        }
        success {
            echo "berhasil nih ngab"
        }
        failure{
            echo "yahh gagal, kenapa tuh?"
        }
        cleanup{
            echo "bersih bersih"
        }
    }
}