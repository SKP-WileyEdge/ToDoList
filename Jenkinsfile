pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Step 1: Clone the repository
                git 'https://github.com/SKP-WileyEdge/ToDoList.git'
            }
        }

        stage('Deploy Web Application') {
            steps {
                // Step 2: Copy files to deployment directory
                cd /root/ToDoList
                sh 'cp -r * /var/www/html'
            }
        }
    }
}
