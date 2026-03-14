pipeline{
    agent{
        label 'AGENT-1'
    }
    options {
        ansiColor('xterm')

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

    }
    post{
        always{
            deleteDir()
        }
    }

}