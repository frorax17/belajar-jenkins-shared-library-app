@Library("belajar-jenkins-shared-library@main") _

import programmerzamannow.jenkins.Output;

pipeline {
    agent any
    stages {
        stage("Library Resource"){
            steps {
                script {
                    def config = libraryResource("config/build.json")
                    echo(config)
                }
            }
        }
        stage("Hello Person"){
            steps {
                script {
                    hello.person([
                        firstName: "Aditya",
                        lastName: "Ayatusy"
                    ])
                }
            }
        }
        stage("Maven Compile"){
            steps {
               script{
                    maven(["clean", "compile", "test"])
               }
            }
        }
        stage("Global Variable"){
            steps {
                echo(author())
                echo(author.name())
                echo(author.channel())
            }
        }
        stage("Hello World"){
            steps {
                script {
                    Output.hello(this, "Aditya")
                }
            }
        }
    }
}
