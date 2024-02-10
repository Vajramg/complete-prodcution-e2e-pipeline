vvpipeline{
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
