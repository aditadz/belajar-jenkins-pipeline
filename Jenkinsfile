pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Start Build'
                sh './mvnw clean compile test-compile'
                echo 'Finish Build'
            }
        }
        stage('Test') {
            steps {
                echo 'Start Test'
                sh './mvnw test'
                echo 'Finish Test'
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