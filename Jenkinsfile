@Library('jenkins-shared-library') _

pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                gitCheckout(
                    branch: "master",
                    url: 'https://github.com/VerticalApps-DevOps/rpa-ex.git'
                )
            }
        }
        stage('Sonar') {
            steps {
                sonarQubeScan()
            }
        }
        stage('Build') {
            steps {
                script {
                    pack() 
                }
            }
        }
        /*stage('Post-Build') {
            steps {
                postBuild()
            }
        }*/
    }
}