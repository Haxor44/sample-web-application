pipeline{
    agent{
        docker{
            image 'maven'
            args '-v $HOME/.m2:/root/.m2'
        }
    }

    stages{
        stage('Check code quality'){
            steps{
                script{
                    withSonarQubeEnv('sonarserver'){
                        sh "mvn sonar:sonar"
                    }
                    timeout(time:1, unit:"HOURS"){
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK'){
                            error "Pipeline aborted"
                        }
                    }
                    sh "mvn clean install"
                }
            }
        }
    }
}