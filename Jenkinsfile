pipeline{
    agent{
        label 'nodes'
        trigger{
            pollSCM('* * * * *')
        }
    }
    stages{
        stage('vcs') {
            steps{
                git url: 'https://github.com/wakaleo/game-of-life.git',
                    branch: 'master'
            }
        }
        stage('build') {
            steps {
                sh 'export PATH="/usr/lib/jvm/java-1.8.0-openjdk-amd64/bin:$PATH" && mvn package'
            }
        }
        stage('Archive artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war', followSymlinks: false,
                junit testResults  '**/target/surefire-reports/TEST-*.xml'
            }
        }        
    }
}