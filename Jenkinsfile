pipeline {
    agent any

//     environment {
//         // Define environment variables
//         MAVEN_HOME = tool 'Maven' // Assuming you've set up Maven tool in Jenkins
//         JAVA_HOME = tool 'JDK17'  // JDK version as required by your project
//     }

    stages {
        stage('Checkout Code') {
            steps {
                // Pull code from Git repository
                git branch: 'main', url: 'https://github.com/RafiouSitou90/demo-jenkins-sonarqube.git'
            }
        }

        stage('Build') {
            agent {
                docker { image 'maven' }
            }
            steps {
                // Clean and build the application
                sh "${MAVEN_HOME}/bin/mvn clean install"
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                sh "${MAVEN_HOME}/bin/mvn test"
            }
        }

        stage('Package') {
            steps {
                // Package the application as a JAR or WAR
                sh "${MAVEN_HOME}/bin/mvn package -Dmaven.test.skip=true"
            }
        }
    }

    post {
        success {
            // Notify success (e.g., via email or Slack)
            echo 'Build and Deployment successful!'
        }
        failure {
            // Notify failure
            echo 'Build or Deployment failed.'
        }
    }
}
