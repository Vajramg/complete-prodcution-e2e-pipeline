pipeline{
    agent{
        label "Jenkins-Agent"
    }
    tools {
     jdk 'java17'
     maven 'Maven3'
     }
    stages{
        stage("Cleanup Workspace"){
            steps{
                cleanWs{}
            }
        }
    }

    stages{
        stage("Checkout from SCM"){
            steps{
                git branch: 'main',credentialId: 'github', url: 'https://github.com/Vajramg/complete-prodcution-e2e-pipeline'
            }

        }
    }
}
}

Jenkins file updated

updated

updated nowfgfdg