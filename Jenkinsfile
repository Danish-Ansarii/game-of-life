pipeline {
    agent { label 'node1' }

    triggers { pollSCM('* * * * *') }

    tools { jdk 'jdk_8' }

    parameters {
        string(name: 'mvn_goal', defaultValue: 'package', description: 'package build')
    }

    environment {
        SONAR_TOKEN = credentials('SONAR_CLOUD') // Store token in Jenkins credentials
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

        stage('SonarCloud Analysis') {
            steps {
                withSonarQubeEnv('SONAR_CLOUD') {
                    sh """
                        mvn sonar:sonar \
                        -Dsonar.projectKey=Kubernetes_Project \
                        -Dsonar.organization=Danish-Ansarii \
                        -Dsonar.host.url=https://sonarcloud.io \
                        -Dsonar.login=$SONAR_TOKEN                    
                    """
                }
            }
        }

        stage('Packages and Tests Reports') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war', followSymlinks: false
                junit '**/target/surefire-reports/TEST-*.xml'
            }
        }

        stage('Quality Gate') {
            steps {
                script {
                    timeout(time: 5, unit: 'MINUTES') {
                        waitForQualityGate abortPipeline: true
                    }
                }
            }
        }
    }
}

