def remote = [:]
remote.name = 'ec2'
remote.host = '78.12.206.86'
remote.user = 'ec2-user'
remote.identityFile = '/var/lib/jenkins/.ssh/id_rsa'
remote.allowAnyHosts = true

pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {

        stage("Clonar código") {
            steps {
                git branch: 'main',
                    url: 'https://github.com/srangelitodev/practica.git'
            }
        }

        stage("Deploy a EC2") {
            steps {
                sshPut remote: remote,
                        from: "${env.WORKSPACE}/*",
                        into: "/home/ec2-user/deploy-temp/"

                sshCommand remote: remote, command: '''
                    sudo rm -rf /usr/share/nginx/html/*
                    sudo cp -r /home/ec2-user/deploy-temp/* /usr/share/nginx/html/
                    sudo chown -R nginx:nginx /usr/share/nginx/html/
                    sudo systemctl reload nginx
                '''
            }
        }
    }
}