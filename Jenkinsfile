pipeline {
    agent any

    triggers {
        // Auto-trigger when changes push ho GitHub main branch
        pollSCM('* * * * *') // Every minute for testing, production main adjust karo
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/A-B-USERS/ultralytics.git',
                    credentialsId: 'github-token2' // Jo PAT tumne Jenkins me add kiya
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                if [ -f composer.json ]; then
                    echo "Composer project detected"
                    composer install --no-dev || true
                else
                    echo "No composer.json found"
                fi
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                if [ -d application/tests ]; then
                    echo "Running PHP Unit Tests"
                    vendor/bin/phpunit --testdox || true
                else
                    echo "No tests found"
                fi
                '''
            }
        }

        stage('Build Artifact') {
            steps {
                sh '''
                mkdir -p build
                # Copy all files except build folder itself
                shopt -s extglob
                cp -r !(build) build/
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                echo "Deploy step — yahan tum apna SCP/SSH/Docker command lagao"
                '''
            }
        }
    }
}
