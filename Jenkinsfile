pipeline {
    agent {
        label 'node1'
    }
    triggers { pollSCM('* * * * *') }

    tools { 
        jdk 'jdk_8' 
    }
    parameters {
         string(name: 'mvn_goal', defaultValue: 'package', description: 'package build')
    

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
}
