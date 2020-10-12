pipeline{
    agent{label 'master'}
    tools{
        maven 'M3'
    }
    stages{
        stage('Checkout'){
            steps{
                git 'https://github.com/nith-art/Digital-Bank.git'
            }
        }
        stage('Build'){
            steps{
                 sh 'mvn clean compile'
            }
        }
        stage('Test'){
            steps{
                     sh 'mvn test'
                     junit '**/target/surefire-reports/TEST-*.xml'
            }
        }
        stage('Package'){
            steps{
                sh 'mvn package'
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
        stage('Deploy'){
            steps{
                input 'Do you approve the deployment?'
		//sh 'scp /var/lib/jenkins/workspace/SpringPetclinic/target/*.jar produser@45.76.96.139:/home/produser'
		//sh 'scp /var/lib/jenkins/workspace/SpringPetclinic/Dockerfile produser@45.76.96.139:/home/produser'
		sh 'docker build . -t digibank'
		sh 'docker run -d --name DigitalBank1 -p 8085:8080 digibank'
            }
        }   
    }
}
