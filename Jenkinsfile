@Library('jenkins-shared-library@master') _

pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                gitCheckout(
                    branch: "${env.GIT_BRANCH}",
                    url: "${env.GIT_URL}"
                )
            }
        }
        //stage('Sonar') {
       //     steps {
        //        sonarQubeScan()
      //      }
       // }
        stage('Build') {
            steps {
                script {
                    pack() 
                }
            }
        }
        stage('Orch Publish') {
            steps {
                script {
                    orchPublish("USCIS-RPA-COE") 
                }
            }
        }
        stage('Post-Build') {
            steps {
                postBuild()
            }
        }
    }
}
