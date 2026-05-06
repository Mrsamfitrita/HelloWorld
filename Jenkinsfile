pipeline {
    agent any

    stages {
        // "Статический анализ" - встроенными средствами Maven
        stage('Static Code Analysis') {
            steps {
                bat 'mvn checkstyle:check'
                echo '✓ Статический анализ выполнен'
            }
        }

        // Сборка
        stage('Build') {
            steps {
                bat 'mvn clean compile'
            }
        }

        // "Хранение в двоичном репозитории" - архивируем прямо в Jenkins
        stage('Archive binary') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                echo '✓ Артефакт сохранён в Jenkins'
            }
        }
    }
}