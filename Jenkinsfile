pipeline {
    agent{
        label "linux && java11"
    }

    environment {
        AUTHOR = "Aditya Ayatusy Syifa"
        EMAIL = "adityaayatusy@gmail.com"
        APP = credentials("aditya_rahasia")
    }
    // triggers{
        // cron("*/1 * * * *")
        // pollSCM("*/1 * * * *")
        
    // }

    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "What is your name")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Neet to Deploy?")
        choice(name: "SOCIAL_MEDIA", choices: ['Instagram', 'Facebook', 'Twitter'], description: "Wich Social Media?")
        password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
    }
    // agent none
    stages {
        stage("Preparation") {
            stages {
                stage("Prepare Java") {
                    steps {
                        echo("Prepare Java")
                    }
                }

                stage("Prepare Maven") {
                    steps {
                        echo("Prepare Manve")
                    }
                }
            }
        }

        stage("Parameters"){
            steps {
                echo "Hello ${params.NAME}"
                echo "You description is ${params.DESCRIPTION}"
                echo "Your social medis is ${params.SOCIAL_MEDIA}"
                echo "Need to deploy ${params.DEPLOY} to deploy !"
                echo "Your secret is ${params.SECRET}"
            }   
        }
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

            input {
                message "Can we deploy?"
                ok "Yes, of course"
                submitter "pzn, aditya"
                parameters {
                    choice (name: "TARGET_ENV", choices: ['DEV', 'QA', 'PROD'], description: "Which Environment?" )
                }
            }
            steps{
                echo("Hello Deploy")
                echo("Target Deploy ${TARGET_ENV}")
                sleep(5)
                echo("Hello Deploy 2")
            }
        }

        stage("Release"){
            
            when {
                expression {
                    return params.DEPLOY
                }
            }

            steps{
                echo("Release it")
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