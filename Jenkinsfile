pipeline{
    agent{
        label 'jdk_8node'
    }
    triggers{
            pollSCM('* * * * *')
        }
     environment {
    SONAR_TOKEN ='9e219b631864ebf87bf14f4f34df981d48c327dd'
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

        // stage('SonarQube Analysis') {
        //     steps {
        //         sh 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=gol-fs_gameoflife'
        //     }

        // }

        stage('SonarQube analysis') {
            withSonarQubeEnv(credentialsId: '9e219b631864ebf87bf14f4f34df981d48c327dd', installationName: 'gol-fs_gameoflife') { // You can override the credential to be used
            sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
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
