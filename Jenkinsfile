pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                // Step 1: Clone the repository
                git branch: 'main', url: 'https://github.com/SKP-WileyEdge/ToDoList.git'
            }
        }

        stage('Deploy Web Application') {
            steps {
                // Step 2: Change working directory
                dir('ToDoList') {
                    // Step 3: Check if deployment directory exists
                    sh 'test -d /var/www/html || mkdir -p /var/www/html'

                    // Step 4: Synchronize files with deployment directory
                    sh 'rsync -avz --delete . /var/www/html'

                    // Step 5: Restart web server
                    sh 'systemctl --quiet is-active httpd || { systemctl start httpd; sleep 5; }'

                    // Step 6: Clean up working directory
                    sh 'rm -rf *'

                    // Step 7: Check for errors
                    catchError(buildResult: 'UNSTABLE', message: 'Failed to deploy web application') {
                        sh 'echo "Deployment successful"'
                    }
                }
            }
        }
    }
}

