pipeline {
    agent{
        label "linux && java11"
    }
    // agent none
    stages {
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