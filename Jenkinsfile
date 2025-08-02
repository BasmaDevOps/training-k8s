pipeline {
    agent any
    stages {
        //Continuous Integration
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        //Continuous Delivery
        stage('Docker Build&Push') {
            steps {
                withDockerRegistry(credentialsId: 'docker', url: "") {
                    sh 'docker build -t basmaoueslati/compare-appt2025 .'
                    sh 'docker push basmaoueslati/compare-appt2025'
                }
            }
        }
        //Continuous Deployment
        stage('Deploy') {
            steps {
                withKubeConfig(credentialsId: 'kubeconfig') {
                    sh "kubectl apply -f compare-app.yaml"
                }
            }  
        }

    }
}

