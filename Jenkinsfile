pipeline {
    agent {
        label 'ansible'
    }
    stages {
        stage('PreTask | Clear work_dir') {
            steps {
                deleteDir()
            }
        }
        stage('Get repo from Git') {
            steps {
                dir('vector-role') {
                    git branch: 'main', url: 'https://github.com/InfernoFeniks/ansible-vector.git'
                }
            }
        }
        stage('Install tools') {
            steps {
                sh "pip3 install 'molecule' 'molecule_docker' 'urllib3==1.26.16'"
                sh "pip3 install -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com  cryptography==36.0.2"
                sh "pip3 install 'requests'"
            }
        }
        stage('Check molecule install') {
            steps {
                sh "molecule --version"
            }
        }
        stage('Start molecule test for docker scenario') {
            steps {
                dir('vector-role') {
                        sh "molecule test -s docker --destroy always"
                }
            }
        }
        stage('Clear work dir after') {
            steps {
                dir('vector-role') {
                    deleteDir()
                }
            }
        }
    }
}
