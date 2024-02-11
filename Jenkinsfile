pipeline{
    agent{
        label "	Jenkins-Agent"
    }
    tools {
        jdk 'Java17'
        Maven 'Maven3'
    }

    stages{
        stage("Cleanup Workspace"){
            steps{
            cleanws()
            }
    }

    stage ("Checkout from SCM"){
    steps{
        git branch: 'main', credentialId: 'github', url: 'https://github.com/Vajramg/complete-prodcution-e2e-pipeline.git'
    }
}

stage ("Building Application"){
    steps{
        mvn clean package
    }
}


