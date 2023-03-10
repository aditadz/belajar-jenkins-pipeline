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

    // triggers {
    //     pollSCM("*/5 * * * *")
    // }

    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "what is your name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "desc you please ")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "need to deploy?")
        choice(name: "SLAVE", choices: ['Kube', 'Swarm', 'On-Premise'], description: "which place to deploy?")
        password(name: "SECRET", defaultValue: "Guest", description: "encrypt key")

    }

    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
    }

    stages {

        stage("OS Setup"){
            matrix{
                axes{
                    axis{
                        name "OS"
                        values "linux", "windows", "mac"
                    }
                    axis{
                        name "ARC"
                        values "32", "64"
                    }
                }

                excludes {
                    exclude {
                        axis {
                            name "OS"
                            values "mac"
                        }
                        axis {
                            name "ARC"
                            values "32"
                        }
                    }
                }

                
            stages{
                
                stage("OS Setup"){
                    agent {
                 node { 
                    label "linux && java11"
                  }
              }
              steps{
                echo "Setup ${OS} ${ARC}"
              }
                } 
            }
            }


        }


        stage ('Preparation') {
            
              parallel {
                stage("Prepare Java"){

                    agent {
                 node { 
                    label "linux && java11"
                  }
              }

                    steps{
                        echo ("prepare java")
                        sleep(5)
                    }
                }

                    stage("prepare maven") {

                        agent {
                 node { 
                    label "linux && java11"
                  }
              }

                steps {
                    echo("prepare maven")
                    sleep(5)
                }
              }
              }
              


        }

        stage('Parameter') {
             agent {
                 node {
                    label "linux && java11"
                  }
              }

            steps {
                echo "Hello ${params.NAME}!"
                echo "You description ${params.DESCRIPTION}!"
                echo "that is ${params.SLAVE} orchestration!"
                echo "Need to deploy: ${params.DEPLOY} to deploy!"
                echo "You secret is ${params.SECRET}!"
            }

        }

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

            input {
                message "can we deploy?"
                ok "yes, of course"
                submitter "adit,adz"
                parameters {
                    choice(name: "TARGET_ENV", choices: ['DEV', 'QA', 'PROD'], description: "Which Environment?")
                }
            }

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
                echo ("Deploy to ${TARGET_ENV}")
                
            }
        }

        stage('Release') {
            when {
                expression {
                    return params.DEPLOY
                }
            }

            agent {
                 node {
                    label "linux && java11"
                    }
                 }
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "adit_rahasia",
                    usernameVariable: "USER",
                    passwordVariable: "PASSWORD"
                )]){
                    sh ('echo "Release it with -u $USER -P $PASSWORD" > "release.txt"')
                }
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