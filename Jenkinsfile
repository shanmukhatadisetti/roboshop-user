pipeline{
    agent{
        label 'AGENT-1'
    }
    options {
        ansiColor('xterm')
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()

    }
    environment{
        appVersion=''
    }
    stages{
        stage('Read Package.json'){
            steps{
                script{
                    def packageJSON = readJSON file: 'package.json'
                    appVersion = packageJSON.version
                    echo "appVersion=${appVersion}"
                }
            }
        }
        stage('Install Dependencies'){
            steps{
                script{
                    sh"""
                        npm install
                    """
                }
            }
        }
        stage('unit testing'){
            steps{
                script{
                    echo "Unit testing"
                }
            }
        }
        stage('Sonar Scan'){
            environment{
                scannerHome = tool 'sonar8.0'
            }

            steps{
                script{
                    withSonarQubeEnv(installationName: 'sonar8.0') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }

    }
    post{
        always{
            deleteDir()
        }
    }

}