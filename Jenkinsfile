pipeline {
    agent any
    parameters {
        choice(name : 'NUMBER,
               choice: [10,20,30,40,50],
               description: 'Select the Num')
    }
    options {
        buildDiscarder(logRotator(daysToKeepStr: '10', numToKeepStr: '10'))
        timeout(time: 12, unit: 'HOURS')
        timestamps()
    }
    triggers {
        cron '@midnight'
    }
    stages {
        stage('Make executable') {
            steps {
                sh('chmod +x ./scripts/fibonacci.sh')
            }
        }
        stage('Relative Path') {
            steps {
                sh("./scripts/fibonacci.sh ${env.NUMBER}")
            }
        }
        stage('Full Path') {
            steps {
                sh("${env.WORKSPACE}/scripts/fibonacci.sh ${env.NUMBER}")
            }
        }

        stage('Change Directory') {
            steps {
                dir("${env.WORKSPACE}/scripts") {
                    sh("./fibonacci.sh ${env.NUMBER}")
                }
            }
        }
    }
}