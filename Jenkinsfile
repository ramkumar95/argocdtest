pipeline {
    agent any
    stages {
        
        stage ('cleanup')  {
            steps {
             cleanWs()
            }
        }

          stage(build) {
            steps {
             cleanWs()
            }
        }
    }
}