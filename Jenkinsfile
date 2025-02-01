pipeline {
    agent {
        label 'node1'
    }
    triggers { pollSCM('* * * * *') }

    tools { 
        jdk 'jdk_8' 
    }

    stages {
        stage('VCS') {
            steps {
                git url: 'https://github.com/Danish-Ansarii/game-of-life.git', branch: 'declerative'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn package'
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
