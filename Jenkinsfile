pipeline{
    agent{
        label 'nodes'
    }
    triggers{
            pollSCM('H/15 * * * 1-5')
        }
    stages{
        stage('vcs') {
            steps{
                git url: 'https://github.com/Danish-Ansarii/game-of-life.git',
                    branch: 'cron'
            }
        }
        stage('build') {
            steps {
                sh 'export PATH="/usr/lib/jvm/java-1.8.0-openjdk-amd64/bin:$PATH" && mvn package'
            }
        }
        stage('Archive artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war'
                junit   '**/target/surefire-reports/TEST-*.xml'
            }
            
        }        

    }
}
