pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out the code from your GitHub repository
                git url: 'https://github.com/japuter/TempConverter', branch: 'master'
            }
        }

        stage('Build') {
            steps {
                // Run Maven build
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run tests using Maven
                sh 'mvn test'
            }
        }

        stage('Code Coverage') {
            steps {
                // Generate and process JaCoCo code coverage report
                jacoco execPattern: '**/target/jacoco.exec'
            }
        }
    }

    post {
        always {
            // Publish JUnit test results
            junit '**/target/surefire-reports/*.xml'

            // Publish JaCoCo code coverage report
            jacoco execPattern: '**/target/jacoco.exec'
        }
    }
}
