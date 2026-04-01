pipeline {
    agent {
        label 'for-testing-ci'
    }

    parameters {
        choice(name: 'RUN_TEST', choices: ['Yes', 'No'], description: 'Yes: unittest + coverage report; No: unittest only')
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Kéo code từ branch main
                git branch: 'main', url: 'https://github.com/nguyenhung5577/demo_ci_main.git'
            }
        }
        stage('Setup Environment') {
            steps {
                echo 'Create virtual environment and install dependencies'
                sh '''
                python3 -m venv .venv
                . .venv/bin/activate
                pip install --upgrade pip
                pip install ruff coverage
                '''
            }
        }
        stage('Lint with Ruff') {
            steps {
                echo 'Lint with Ruff'
                sh '''
                . .venv/bin/activate
                ruff check .
                '''
            }
        }
        stage('Coverage report') {
            when {
                expression {
                    return params.RUN_TEST == 'Yes'
                }
            }
            steps {
                echo 'Coverage report'
                sh '''
                . .venv/bin/activate
                coverage run -m unittest test_main.py -v
                coverage report -m
                '''
            }
        }
        stage('Test') {
            when {
                expression {
                    return params.RUN_TEST == 'No'
                }
            }
            steps {
                sh '''
                . .venv/bin/activate
                python -m unittest test_main.py -v
                '''
            }
        }
    }
}
