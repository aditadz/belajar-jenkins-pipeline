pipeline {
    agent none
    // agent {
    //     node {
    //         label "linux && java11"
    //     }
    // }

    stages {
        stage('Build') {
            agent {
                 node {
                    label "linux && java11"
                  }
              }
            steps {

                script {
                    for (int i = 0; i < 10; i++) {
                        echo ("script ${i}")
                    }
                }

                echo 'Start Build'
                sh './mvnw clean compile test-compile'
                echo 'Finish Build'
            }
        }
        stage('Test') {
            agent {
                 node {
                    label "linux && java11"
                  }
                 }
            steps {
                
                script {
                    def data = [
                        "firstName": "Adit",
                        "lastName" : "Abdul Azis"
                    ]
                    writeJSON(file: "data.json", json: data)
                }
                echo 'Start Test'
                sh './mvnw test'
                echo 'Finish Test'
            }
        }
         stage('Deploy') {
            agent {
                 node {
                    label "linux && java11"
                  }
                 }
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