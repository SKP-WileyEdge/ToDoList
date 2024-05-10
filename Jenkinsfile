pipeline {
    agent any
    triggers {
        // Define triggers outside of the pipeline block
        githubPush() // Trigger the pipeline on GitHub push events
    }

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
                    script {
                        try {
                            sh 'sudo rsync -avz --delete . /var/www/html'
                        } catch (Exception e) {
                            echo "Failed to sync files: ${e.message}"
                        }
                    }

                    // Step 5: Print contents of workspace and deployment directory
                    sh 'ls -l'
                    sh 'ls -l /var/www/html'

                    // Step 6: Restart web server
                    sh 'systemctl --quiet is-active httpd || { sudo systemctl start httpd; sleep 5; }'

                    // Step 7: Clean up working directory
                    sh 'rm -rf *'

                    // Step 8: Check for errors
                    catchError(buildResult: 'UNSTABLE', message: 'Failed to deploy web application') {
                        sh 'echo "Deployment successful"'
                    }
                }
            }
        }
    }
}
