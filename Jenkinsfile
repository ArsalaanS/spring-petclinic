pipeline {
    agent any

    triggers {
        cron('H/5 * * * *')
    }

    stages {

        stage('Build, Test & Coverage') {
            steps {
                sh 'chmod +x mvnw'
                sh './mvnw clean verify'
            }
        }
    }

    post {
        always {
            jacoco(
                execPattern: 'target/jacoco.exec',
                classPattern: 'target/classes',
                sourcePattern: 'src/main/java'
            )
        }

        success {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}
