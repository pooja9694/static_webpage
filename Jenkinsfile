pipeline {

agent any

environment {
DOCKERHUB = "yourdockerhubusername/static-web"
}

stages {

stage('Clone Repository') {
steps {
git 'https://github.com/yourusername/project.git'
}
}

stage('Build Docker Image') {
steps {
sh 'docker build -t $DOCKERHUB .'
}
}

stage('Push Docker Image') {
steps {
withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {

sh '''
docker login -u $USER -p $PASS
docker push $DOCKERHUB
'''
}
}
}

stage('Deploy using Ansible') {
steps {
sh 'ansible-playbook -i hosts deploy.yml'
}
}

}

}