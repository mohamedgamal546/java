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
        stages("Build java   app") {
            steps{
                sh "mvn package install -DskipTests"
            }
        }
        stages("Test java app") {
            steps{
                sh "mvn test"
            }
        }
        stages("Archive java app") {
            steps{
                archiveArtifacts artifacts: '**/*.jar', followSymlinks: false
            }
        }
        stages("Build docker image ") {
            steps{
                sh "docker build -t java-app:v1 . "
            }
        }
        stages("Docker Login ") {
            steps{
                sh "docker login  -u ${dockerUsername} -p ${dockerpassword} "
            }
        }      
        // stages("Push docker image ") {
        //    steps{
        //        sh "docker push java-app:v1 "
        //    }
        //}          
    } 
}

