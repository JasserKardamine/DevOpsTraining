pipeline {
    agent any
    
    options {
        timeout(time: 1, unit: 'HOURS')
    }
    
    environment {
        APP_ENV = "DEV"
    }
    
    stages {
        stage('Code Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Package') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }
    
    post {
        success {
            mail(
                to: 'jasserhav@gmail.com',
                subject: "Jenkins: Build Successful!",
                body: "Good news! Your build succeeded!"
            )

            echo "Pipeline executed smtp config"
        }
        failure {
            mail(
                to: 'jasserhav@gmail.com',
                subject: "Jenkins: Build Failed",
                body: "Oops! Your build failed. Check Jenkins console for details."
            )
            echo "Pipeline execution failed"
        }
    }

}