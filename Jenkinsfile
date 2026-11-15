
pipeline {
    agent any

    environment {
        REGISTRY = '194.199.106.9:5000'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Code source récupéré depuis GitHub'
            }
        }

        stage('Build calc-service') {
            steps {
                dir('calc-service') {
                    sh 'docker build -t $REGISTRY/calculator-calc:latest .'
                }
            }
        }

        stage('Build sum-service') {
            steps {
                dir('sum-service') {
                    sh 'docker build -t $REGISTRY/calculator-sum:latest .'
                }
            }
        }

        stage('Build sub-service') {
            steps {
                dir('sub-service') {
                    sh 'docker build -t $REGISTRY/calculator-sub:latest .'
                }
            }
        }

        stage('Build mul-service') {
            steps {
                dir('mul-service') {
                    sh 'docker build -t $REGISTRY/calculator-mul:latest .'
                }
            }
        }

        stage('Build div-service') {
            steps {
                dir('div-service') {
                    sh 'docker build -t $REGISTRY/calculator-div:latest .'
                }
            }
        }

        stage('Push images') {
            steps {
                sh 'docker push $REGISTRY/calculator-calc:latest'
                sh 'docker push $REGISTRY/calculator-sum:latest'
                sh 'docker push $REGISTRY/calculator-sub:latest'
                sh 'docker push $REGISTRY/calculator-mul:latest'
                sh 'docker push $REGISTRY/calculator-div:latest'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f kubernetes/'
            }
        }
    }

    post {
        success {
            echo 'Toutes les images ont été construites et publiées avec succès !'
        }
        failure {
            echo 'Échec du pipeline.'
        }
    }
}
