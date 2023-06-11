pipeline{
    agent any
    tools{
        maven "MAVEN3"
        jdk "JDK8"
    }
    stages{
        stage('BUILD'){
            steps{
                sh 'mvn install'
            }
            post{
                success{
                    echo "archiving the artifact"
                    archiveArtifacts artifacts: '**/*.war'
                    
                }
            }
        }
        stage('Unit Test'){
            sh 'mvn test'
        }
                stage('Check Style'){
            sh 'mvn checkstyle:checkstyle'
        }
    }
}