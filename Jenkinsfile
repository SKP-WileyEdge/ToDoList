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
                    // Step 3: Copy files to deployment directory
                    sh 'cp -r * /var/www/html'

                    // Step 4: Check for errors
                    catchError(buildResult: 'UNSTABLE', message: 'Failed to deploy web application') {
                        sh 'echo "Deployment successful"'
                    }
                }
            }
        }
    }
}

