pipeline {
    agent {
        label 'ubuntu_node'
    }
    triggers {
        cron('H */4 * * 1-5')
    }
    
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
        
        stage('Package and Test Reports') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war', followSymlinks: false
                junit '**/target/surefire-reports/TEST-*.xml'
            }
        }
    }
}
