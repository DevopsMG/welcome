pipeline{
    
    agent any
    
    stages{
        stage('checkout')
        {
            steps{
                checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/DevopsMG/SpringProjectforCICD']]]
            }
        }
        stage('build artifact')
        {
            steps{
                echo 'using maven to build the artifact'
                sh "mvn clean package"
                sh "cp target/ebstack-0.0.1-SNAPSHOT.jar /home/devopsuser/"
                sh "java -jar /home/devopsuser/ebstack-0.0.1-SNAPSHOT.jar"
            }
        }
        stage('Tests')
        {
            steps{
                echo 'running the system test cases'
                sh "curl -X GET http://localhost:8085/api/v1/users/create"
            }
        }
    }
    
    
}
