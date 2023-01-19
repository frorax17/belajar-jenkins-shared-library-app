pipeline {
    agent{
        label "linux && java11"
    }

    environment {
        AUTHOR = "Aditya Ayatusy Syifa"
        EMAIL = "adityaayatusy@gmail.com"
        APP = credentials("aditya_rahasia")
    }
    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'SECONDS')
    }
    // agent none
    stages {
        stage("Prepare"){
            steps{
                echo("Author : ${AUTHOR}")
                echo("Email : ${EMAIL}")
                echo("App User : ${APP_USR}")
                // sh("echo 'App Password : ${APP_PSW}' > 'rahasia.txt'")
                sh('echo "App Password : ${APP_PSW}" > "rahasia1.txt"')
                echo("Start Job : ${env.JOB_NAME}")
                echo("Start Build : ${env.BUILD_NUMBER}")
                echo("Branch Name : ${env.BRANCH_NAME}")
            }
        }
        stage("Build"){
            // agent{
            //     label "linux && java11"
            // }
            steps{
                script{
                    for(int i = 0; i < 10; i++){
                        echo("Script ${i}")
                    }
                }
                echo("Start Build")
                sh("./mvnw clean compile test-compile")
                echo("Finish Build")
            }
        }

        stage("Test"){
            steps{
                // agent{
                //     label "linux && java11"
                // }
                script{
                    def data = [
                        "firstName": "Aditya",
                        "lastName": "Ayatusy"
                    ]

                    writeJSON(file: "data.json", json: data)
                }
                echo("Start Test")
                sh("./mvnw test")
                echo("Finish Test")
            }
        }

        stage("Deploy"){
            // agent{
            //     label "linux && java11"
            // }
            steps{
                echo("Hello Deploy")
                sleep(5)
                echo("Hello Deploy 2")
            }
        }
    }

    post {
        always{
            echo "I will always say Hello again!"
        }
        success{
            echo "Yay, success"
        }
        failure{
            echo "Oh no, failure"
        }
        cleanup{
            echo "Don't care success or error"
        }
    }
}