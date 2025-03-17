pipeline {
    agent any

   
    stages {
        
        stage('Build') {
            steps {
                script {
                    echo "docker build"
                    if (env.GIT_BRANCH == 'origin/dev') {
                        sh 'docker build -t jp/dev:latest .'
                    } else if (env.GIT_BRANCH == 'origin/main') {
                        sh 'docker build -t jayaprakadeesh/prod:latest .'
                    }
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    sh 'docker login -u "jayaprakadeesh" -p "$Docker_pass" docker.io'
                    if (env.GIT_BRANCH == 'origin/dev') {
                        sh 'docker push jayaprakadeesh/dev:latest'
                    } else if (env.GIT_BRANCH == 'origin/main') {
                        sh 'docker push jayaprakadeesh/prod:latest'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh 'docker ps -aq | xargs -r docker rm -f'
                    if (env.GIT_BRANCH == 'origin/dev') {
                        sh 'docker run -d -p 800:80 jayaprakadeesh/dev:latest'
                    } else if (env.GIT_BRANCH == 'origin/main') {
                        sh 'docker run -d -p 80:80 jayaprakadeesh/prod:latest'
                    }
                }
            }
        }
        stage('Cleanup') {
            steps {
                script {
                    sh 'docker image prune -f'
                }
            }
        }
    }
}
