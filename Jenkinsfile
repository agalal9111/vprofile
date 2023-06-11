pipeline{
    agent any
    tools{
        maven "MAVEN3"
        jdk "JDK8"
    }
        environment {
        registry = "agalal9111/vproappdock"
        registryCredential = 'dockerhub'
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
                               /*  stage('Sonar Analaysis'){
                                    environment{
                                        scannerHome = tool 'sonar4.8'
                                    }
            steps{
              withSonarQubeEnv('sonar') {
                   sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                   -Dsonar.projectName=vprofile \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
              }
            }
        }*/

                stage('Build App Image') {
          steps {
            script {
              dockerImage = docker.build registry + ":V$BUILD_NUMBER"
            }
          }
        }

                stage('Upload Image'){
          steps{
            script {
              docker.withRegistry('', registryCredential) {
                dockerImage.push("V$BUILD_NUMBER")
                dockerImage.push('latest')
              }
            }
          }
        }       

    }
}