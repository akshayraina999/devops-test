pipeline{
    agent any
    tools{
        maven '3_5_0'
    }
    stages{
        stage('Quality Gate Status Check'){
            steps{
                script{
                    withSonarQubeEnv('sonarserver'){
                        sh "mvn sonar:sonar"
                    }
                    timeout(time:1, unit: 'HOURS'){
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK'){
                            error "Pipeline aborted due to quality gate failure: ${qg.staus}"
                        }
                    }
                    sh "mvn clean install"
                }
            }
        }
        // stage('build'){
        //     steps{
        //         script{
        //             sh 'cp -r ../devops'
        //         }
        //     }
        // }
    }
}