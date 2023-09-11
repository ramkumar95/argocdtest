pipeline {
    agent any
    environment {
      APP_NAME = "jenkins"
    }
    stages {
        
        stage ('cleanup')  {
            steps {
             cleanWs()
            }
        }

        stage("Checkout from SCM") {
            steps {
                git branch: 'main', url: 'https://github.com/ramkumar95/argocdtest'
            }
        }
    

    
        stage("Update the Deployment Tags") {
            steps {
                sh """
                    cat deployment.yaml
                    sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                    cat deployment.yaml
                """
            }
        }

    }
}
