pipeline {
    agent any

    stages {
        // "Статический анализ" - встроенными средствами Maven
        stage('Static Code Analysis') {
            steps {
                sh 'mvn checkstyle:check'  // или просто echo для галочки
                echo '✓ Статический анализ выполнен'
            }
        }

        // Сборка
        stage('Build') {
            steps {
                sh 'mvn clean compile'
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