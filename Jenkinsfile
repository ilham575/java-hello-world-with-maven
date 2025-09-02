pipeline {
    agent any

    stages {
        stage('Maven Check') {
            steps {
                sh 'docker run -i --rm --name my-maven-project maven:3.9.9 mvn --version'
            }
        }
        stage('Build') {
            steps {
                sh 'docker run -i --rm --name my-maven-project -v "E:\\Mobile_app\\jenkins_lab\\java-hello-world-with-maven:/usr/src/mymaven" -w /usr/src/mymaven maven:3.9.9 mvn clean install'
            }
        }
        stage('SonarQube') {
            steps {
                sh '''
                docker run -i --rm --name my-maven-project \
                  -v "E:\\Mobile_app\\jenkins_lab\\java-hello-world-with-maven:/usr/src/mymaven" \
                  -w /usr/src/mymaven maven:3.9.9 \
                  mvn clean verify sonar:sonar \
                  -Dsonar.projectKey=Myapp \
                  -Dsonar.projectName="Myapp" \
                  -Dsonar.host.url=http://172.17.0.3:9000 \
                  -Dsonar.token=sqa_875067b06ba40fae4116c3054a1708882d00b15c
                '''
            }
        }
    }
}
