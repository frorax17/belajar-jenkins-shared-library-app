@Library("belajar-jenkins-shared-library@main") _

import programmerzamannow.jenkins.Output;

pipeline {
    agent any
    stages {
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
