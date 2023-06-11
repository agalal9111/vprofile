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
            steps{
                    sh 'mvn test'
            }
            
        }
                stage('Check Style'){
                    steps{
                        sh 'mvn checkstyle:checkstyle'
                    }
            
        }
    }
}