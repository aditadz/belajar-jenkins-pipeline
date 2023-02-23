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
                sleep(5)
                echo 'Building Maven Apps 2'
                echo 'Building Maven Apps 3'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing Maven Apps'
                sleep(5)
                echo 'Testing Maven Apps 2'
                echo 'Testing Maven Apps 3'
               // sh 'error'
            }
        }
         stage('Deploy') {
            steps {
                echo 'Deploying Maven Apps'
                sleep(5)
                echo 'Deploying Maven Apps 2'
                echo 'Deploying Maven Apps 3'
                
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