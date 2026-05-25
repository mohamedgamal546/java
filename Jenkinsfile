@Library('sys-lib')



pipeline{
    agent {
       label 'jenkins-agent-01'
    }

     tools {
       jdk 'jdk-11'
       maven 'maven-354'
    }

    environment {
       dockerUsername = credentials("dockerUsername")
       dockerpassword = credentials("dockerpassword")
    }
    stages{
        stage("Build java app") {
            steps{
                script {
                    def r7 = new edu.iti.mavenClass()
                    r7.Build("package install -DskipTests")
                }
            }
        }
        stage("Test java app") {
            steps{
                script {
                    def r7 = new edu.iti.mavenClass()
                    r7.test()
                }
            }
        }
        stage("Archive java app") {
            steps{
                archiveArtifacts artifacts: '**/*.jar', followSymlinks: false
            }
        }
        stage("Build docker image ") {
            steps{
                script {
                    def r9 = new edu.iti.dockerClass()
                    r9.build("mohamedgamal5466/java","v${BUILD_NUMBER}")  
                }
            } 
        }
        stage("Docker Login ") {
            steps{
                              script {
                    def r9 = new edu.iti.dockerClass()
                    r9.login("${dockerUsername}","${dockerpassword}")  
                }
            }
        }      
        // stage("Push docker image ") {
        //    steps{
        //        sh "docker push mohamedgamal5466/java:v${imageTag} "
        //    }
        //}          
    } 
}

