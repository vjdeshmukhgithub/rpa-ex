@Library('rpa-sharedlib@master') _

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
        stage('IQ Server') {
            steps {
                script {
                    
                    try {
                        nexusPolicyEvaluation advancedProperties: '', failBuildOnNetworkError: false, iqApplication: selectedApplication('uipath'), iqStage: 'build', jobCredentialsId: ''
                      } catch (error) {
                        throw error
                      }
                    
                    
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
