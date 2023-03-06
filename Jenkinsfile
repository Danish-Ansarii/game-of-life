pipeline {
    agent { label 'builtin' }
    triggers { pollSCM ('H/15 * * * *') }
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['package', 'install', 'clean'], description: 'Maven Goal')
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/Danish-Ansarii/game-of-life.git',
                    branch: 'master'
            }
        }
        stage('package') {
            tools {
                jdk 'jdk_8'
            }
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
            }
        }
        stage('copy build') {
            steps {
                sh 'mkdir -p /tmp/$JOB_NAME/${BUILD_ID} && cp ./gameoflife-web/target/gameoflife.war /tmp/$JOB_NAME/${BUILD_ID}/'
            }
        }
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
        post{
            success {
                mail 
                    subject: "THis is subject of project ${JOB_NAME} SUCCESS"
                    body: "This is the body of mail",
                    to: "team-all-qt@qt.com",
                    from: "devops@qt.com"

            }
            failure {
                mail 
                    subject: "THis is subject of project ${JOB_NAME} FAILURE"
                    body: "This is the body of mail",
                    to: "team-all-qt@qt.com",
                    from: "devops@qt.com"

            }
        }
    }
}
