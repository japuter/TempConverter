pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/japuter/TempConverter', branch: 'master'
            }
        }

        stage('Build') {
            steps {
                // Use 'bat' instead of 'sh' on Windows
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Use 'bat' to run tests
                bat 'mvn test'
            }
        }

        stage('Code Coverage') {
            steps {
                jacoco execPattern: '**/target/jacoco.exec'
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
            jacoco execPattern: '**/target/jacoco.exec'
        }
    }
}
