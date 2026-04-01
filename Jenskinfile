pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                // Kéo code từ branch main
                git branch: 'main', url: 'https://github.com/nguyenhung5577/demo_ci_main.git'
            }
        }
        stage('Test') {
            steps {
                sh 'python3 -m unittest test_main.py -v'
            }
        }
    }
}