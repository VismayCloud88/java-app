library 'my-shared-library'

pipeline {
    agent any
    parameters {
        choice(name: 'action', choices: ['create', 'destroy'], description: 'Choose action')
    }
    stages {
        stage('Git Checkout') {
            steps {
                git_checkout(branch: 'main', url: 'https://github.com/VismayCloud88/java-app.git')
            }
        }
        stage('Unit Test') {
            steps {
                mvn_test()
            }
        }
        stage('Integration Test') {
            steps {
                integration_test_maven()
            }
        }
        stage('Static Code Analysis') {
            steps {
                static_code_analysis(credentialId: 'sonarqube-token-id')
            }
        }
        stage('Quality Gate Check') {
            steps {
                quality_gate_status_check(credentialId: 'sonarqube-token-id')
            }
        }
        stage('Maven Build') {
            steps {
                maven_build()
            }
        }
    }
}
