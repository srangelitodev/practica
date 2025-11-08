pipeline {
    agent any

    stages {
        stage('Clonar código') {
            steps {
                git branch: 'main', url: 'https://github.com/srangelitodev/practica.git'
            }
        }

        stage('Desplegar sitio') {
            steps {
                sh '''
                sudo rm -rf /usr/share/nginx/html/*
                sudo cp -r * /usr/share/nginx/html/
                sudo systemctl reload nginx
                '''
            }
        }
    }
}
