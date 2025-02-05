pipeline {
    agent {
        label 'node1'
    }
    triggers { 
        pollSCM('* * * * *') 
    }

    tools { 
        jdk 'jdk_8' 
    }

    parameters {
        string(name: 'mvn_goal', defaultValue: 'package', description: 'package build')
    }

    stages {
        stage('VCS') {
            steps {
                git url: 'https://github.com/Danish-Ansarii/game-of-life.git', branch: 'declerative'
            }
        }
        
        stage('Build') {
            steps {
                sh "mvn ${params.mvn_goal}"
            }
        }
        
        stage('Packages and Tests Reports') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war', followSymlinks: false
                junit '**/target/surefire-reports/TEST-*.xml'
            }
        }
    }

    // post {
    //     success {
    //         emailext (
    //             subject: "Jenkins Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
    //             body: """
    //                 Good news! 🎉

    //                 The build for job *${env.JOB_NAME}* (Build #${env.BUILD_NUMBER}) was successful.

    //                 Check the console output here: ${env.BUILD_URL}

    //                 Regards,
    //                 Jenkins
    //             """,
    //             to: 'dani@gmail.com'
    //         )
    //     }
    //     failure {
    //         emailext (
    //             subject: "Jenkins Build Failure: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
    //             body: """
    //                 Oops! ❌

    //                 The build for job *${env.JOB_NAME}* (Build #${env.BUILD_NUMBER}) has failed.

    //                 Please check the console output: ${env.BUILD_URL}

    //                 Regards,
    //                 Jenkins
    //             """,
    //             to: 'dani@gmail.com'
    //         )
    //     }
    // }
}
