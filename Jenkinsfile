pipeline{
    agent any
    tools{
        maven "MAVEN3"
        jdk "JDK8"
    }
    stages{
        stage('BUILD'){
            steps{
                sh 'mvn build'
            }
        }
    }
}