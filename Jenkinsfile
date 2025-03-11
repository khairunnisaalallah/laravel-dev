pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    echo 'Checking out repository...'
                    git branch: 'main', url: 'https://github.com/khairunnisaalallah/laravel-dev'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Building application...'
                    // Tambahkan perintah build jika diperlukan, misalnya:
                    // sh './gradlew build'
                    // sh 'mvn package'
                    // sh 'npm install'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    // Tambahkan perintah untuk menjalankan unit test
                    // sh 'npm test'
                    // sh './gradlew test'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying application...'
                    // Tambahkan perintah untuk deploy ke server atau container
                    // sh 'scp target/app.jar user@server:/path/to/deploy'
                    // sh 'docker-compose up -d'
                }
            }
        }

        // Deploy ke environment production
        stage('Deploy to Production') {
            agent any
            steps {
                script {
                    docker.image('agung3wi/alpine-rsync:1.1').inside('-u root') {
                        sshagent (credentials: ['ssh-prod']) {
                            sh 'mkdir -p ~/.ssh'
                            sh 'ssh-keyscan -H "$PROD_HOST" > ~/.ssh/known_hosts'
                            sh "rsync -rav --delete ./laravel/ ubuntu@$PROD_HOST:/home/ubuntu/prod.kelasdevops.xyz/ --exclude=.env --exclude=storage --exclude=.git"
                        }
                    }
                }
            }
        }
    }
}
