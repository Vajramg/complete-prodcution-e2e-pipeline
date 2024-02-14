pipeline {
    agent {
        label "Jenkins-Agent"
    }
    tools {
        jdk 'Java17'
        maven 'Maven3'
        environment= {
            App_Name= "complete-prodcution-e2e-pipeline"
            Docker_User= "vajramg"
            Docker_pass= "dockerhub"
            Image_Name= "${Docker_User}" + "/" + "${App_Name}"
            Image_Tag= "${Release}-${Build Number}"
            Jenkins_API_Token= "credentials("Jenkins_API_Token")

        }
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
     stage("Quality Gate") {
            steps {
              script {
                waitForQualityGate abortPipeline: false, credentialsId: 'sonarqube-token'
              }
            }
        }

    stage("Build Docker and Push Image") {
            steps {
                script {
                docker.withRegistry('', Docker_Pass){
                    docker_image.push("${Image_Tag}")
                        docker_image.push('latest')
                    }

                }
            }
        }
    }
}  