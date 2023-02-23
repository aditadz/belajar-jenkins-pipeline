pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }

    stages {
        stage('Hello') {
            steps {
                echo 'my first pipeline kiww'
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