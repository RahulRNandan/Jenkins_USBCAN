pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/RahulRNandan/Jenkins_USBCAN.git'
            }
        }
        stage('Build') {
            steps {
                dir('embedded_firmware') { 
                    sh 'make'
                }
            }
        }
        stage('Generate Doxygen Documentation') {
            steps {
                dir('docs') {
                    sh 'doxygen Doxyfile'
                }
            }
        }
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'embedded_firmware/bin/*'
            }
        }
        stage('Run Python Tests') {
            steps {
                dir('tests') {
                    sh 'python3 -m unittest discover'
                }
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed.'
        }
    }
}
