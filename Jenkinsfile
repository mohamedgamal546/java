pipeline {
    agent {
        label 'jenkins-agent-01'
    }

    tools {
        jdk 'jdk-11'
        maven 'maven-354'
    }

    stages {

        stage('Build java app') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test java app') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Archive java app') {
            steps {
                archiveArtifacts artifacts: '**/*.jar', followSymlinks: false
            }
        }

        stage('Build docker image') {
            steps {
                sh 'docker build -t java-app:v1 .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-cred',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        // stage('Push docker image') {
        //     steps {
        //         sh 'docker push java-app:v1'
        //     }
        // }
    }
}