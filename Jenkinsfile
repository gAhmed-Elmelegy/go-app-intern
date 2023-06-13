pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub_credentials')
        REPORT_EMAIL = "ahmedelmelegy3570@gmail.com"
    }

    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage('Login to DockerHub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Build image') {
            steps {
                catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                    sh(script: """
                        docker images
                        docker build -t ahmedelmelegy3570/app-multistage .
                    """)
                }
            }
        }
        stage('Push image') {
            steps {
                catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                    sh(script: """
                        docker push r ahmedelmelegy3570/app-multistage
                    """)
                }
            }
        }
    }
    }
}
