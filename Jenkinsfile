pipeline{
    agent{
        label 'jdk_8node'
    }
    triggers{
            pollSCM('* * * * *')
        }
    
    parameters { string(name: 'parameter', defaultValue: 'clean package', description: 'this is use to clean package') }

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

        stage('SonarQube Analysis') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.login=01d6cd64f8f186040722ff45953f4c80f8e102be'
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
