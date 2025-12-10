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
                echo "=====Checking out code from Git====="
                echo "=====trying the webhook trigger ====="
                checkout scm  // Utilise checkout scm au lieu de git
            }
        }
        
        stage('Build Package') {
            steps {
                echo "=====Building Spring Boot application====="
                sh 'mvn clean package -DskipTests'
            }
        }
        
        stage('Archive Artifacts') {
            steps {
                echo "=====Archiving JAR file====="
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }
    
    post {
        always {
            echo "======always======"
        }
        success {
            mail to : 'jasserhav@gmail.com',
                subject: "Jenkins : Build Successful ! "
                body: "Good news ! Your build succeeded !"
            echo "=====pipeline executed successfully ====="
        }
        failure {
             mail to: 'jasserhav@gmail.com',
                 subject: "Jenkins: Build Failed",
                 body: "Oops! Your build failed. Check Jenkins console for details."
            echo "======pipeline execution failed======"
        }
    }
}