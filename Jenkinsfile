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

        stage("Push the changed deployment file to Git") {
            steps {
                sh """
                    git config --global user.name "ram"
                    git config --global user.email "ram@test.com"
                    git add deployment.yaml
                    git commit -m "Updated Deployment Manifest"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'ramkumar95', gitToolName: 'Default')]) {
                    sh "git push https://github.com/ramkumar95/argocdtest/ main"
                }
            }
        }

    }
}
