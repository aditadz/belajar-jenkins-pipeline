pipeline {
    agent none
    // agent {
    //     node {
    //         label "linux && java11"
    //     }
    // }

    environment {
        AUTHOR = "Adit Abdul Azis"
        EMAIL = "aditazis.id@gmail.com "
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'SECONDS')
    }

    stages {

        stage('Prepare') {

            environment {
                APP = credentials("adit_rahasia")
            }
            agent {
                 node {
                    label "linux && java11"
                  }
              }
            steps {
                echo ("Author : ${AUTHOR}")
                echo ("Email : ${EMAIL}")
                echo ("Start Job  : ${env.JOB_NAME}")
                echo ("Start Build  : ${env.BUILD_NUMBER}")
                echo ("Branch Name  : ${env.BRANCH_NAME}")
                echo ("App user : ${APP_USR}")
                echo ("App password : ${APP_PSW}")
                sh ('echo "App Password : ${APP_PSW}" > "rahasia.txt" ')
            }
        }

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