pipeline{
    agent{
        label 'nodes'
    }
    triggers{
            pollSCM('* * * * *')
        }
    
    parameters { string(name: 'PARA', defaultValue: 'clean package', description: 'this is use to clean package') }

    stages{
        stage('vcs') {
            steps{
                git url: 'https://github.com/Danish-Ansarii/game-of-life.git',
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
                archiveArtifacts artifacts: '**/target/gameoflife.war'
                junit   '**/target/surefire-reports/TEST-*.xml'
            }
            
        }        
        

    }

}
