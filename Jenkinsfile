pipeline {
    agent any

    stages {
        stage('Static Code Analysis') {
            steps {
                // Замените URL на адрес вашего запущенного SonarQube
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Publish to Binary Repository') {
            when {
                anyOf { branch 'integration'; branch 'master' }
            }
            steps {
                // Замените URL на адрес вашего Nexus
                nexusPublisher(
                    nexusInstanceId: 'nexus',
                    nexusRepositoryId: 'maven-releases',
                    packages: [
                        [
                            $class: 'MavenPackage',
                            mavenCoordinate: [
                                groupId: 'com.example',
                                artifactId: 'hello-world',
                                version: '1.0.0'
                            ],
                            mavenAssetList: [
                                [
                                    extension: 'jar',
                                    filePath: 'target/*.jar'
                                ]
                            ]
                        ]
                    ]
                )
            }
        }
    }
}