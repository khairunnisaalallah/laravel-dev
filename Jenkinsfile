pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/khairunnisaalallah/laravel-dev'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'composer install --no-interaction --prefer-dist --optimize-autoloader'
            }
        }

        stage('Run Migrations') {
            steps {
                sh 'php artisan migrate --force'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'php artisan test'
            }
        }
    }
}
