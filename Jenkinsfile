pipeline{
    agent {
        docker {
            image 'maven:3-openjdk-11'
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
                            error "Pipeline aborted: ${qg.status}"
                        }
                    }
                    sh "mvn clean install"
                }
            }
        }
    }
}