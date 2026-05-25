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
                sh "mvn package install -DskipTests"
            }
        }
        stage("Test java app") {
            steps{
                sh "mvn test"
            }
        }
        stage("Archive java app") {
            steps{
                archiveArtifacts artifacts: '**/*.jar', followSymlinks: false
            }
        }
        stage("Build docker image ") {
            steps{
                sh "docker build -t mohamedgamal5466/java:v${imageTag} . "
            }
        }
        stage("Docker Login ") {
            steps{
                sh "docker login  -u ${dockerUsername} -p ${dockerpassword} "
            }
        }      
        // stage("Push docker image ") {
        //    steps{
        //        sh "docker push mohamedgamal5466/java:v${imageTag} "
        //    }
        //}          
    } 
}

