pipeline {
    agent any
    
    environment {
        JAVA_HOME = "C:\\Users\\kotik\\.jdks\\corretto-23.0.2"
        MAVEN_HOME = "C:\\maven\\apache-maven-3.9.15-bin\\apache-maven-3.9.15"
        PATH = "${env.JAVA_HOME}\\bin;${env.MAVEN_HOME}\\bin;${env.PATH}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Detect Branch') {
            steps {
                script {
                    echo "Current branch: ${env.BRANCH_NAME}"
                    
                    if (env.BRANCH_NAME == 'main') {
                        echo " Production (main branch)"
                    } 
                    else if (env.BRANCH_NAME == 'integration') {
                        echo " Integration (integration branch)"
                    } 
                    else if (env.BRANCH_NAME.startsWith('feature/')) {
                        echo " Feature branch: ${env.BRANCH_NAME}"
                    }
                }
            }
        }

        stage('Static Code Analysis') {
            steps {
                bat 'mvn checkstyle:check'
                echo '✓ Статический анализ выполнен'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean compile'
                echo '✓ Сборка выполнена'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
                echo '✓ Тесты пройдены'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
                echo '✓ Пакетирование выполнено'
            }
        }
    }
    
    post {
        success {
            echo ' Pipeline SUCCESS '
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            echo '✓ Артефакт сохранён в Jenkins'
        }
        failure {
            echo 'Pipeline FAILED '
        }
    }
}
