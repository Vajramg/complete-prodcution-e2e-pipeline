pipeline {
    agent {
        label "Jenkins-Agent"
    }
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }
        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/Vajramg/complete-prodcution-e2e-pipeline'
            }
        }
        stage("Building Application") {
            steps {
                sh 'mvn clean package'
            }
        }
        stage("Test Application") {
            steps {
                sh 'mvn test'
            }
        }
        stage("Sonarqube Analysis") {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonarqube-token') {
                        sh 'mvn sonar:sonar'
                    }
                }
            }
        }
    }
}
