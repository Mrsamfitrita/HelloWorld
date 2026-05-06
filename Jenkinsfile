pipeline {
    agent any

    environment {
        JAVA_HOME = 'C:\\Program Files\\Java\\jdk-17'
        PATH = "${env.JAVA_HOME}\\bin;${env.PATH}"
    }

    stages {
        stage('Static Code Analysis') {
            steps {
                bat 'mvn checkstyle:check'
                echo '✓ Статический анализ выполнен'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Archive binary') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                echo '✓ Артефакт сохранён в Jenkins'
            }
        }
    }
}
