pipeline {
    agent any
    environment {
    	SRC_DIR = "${env.WORKSPACE}"
    }
    stages {
        stage('Build') {
            parallel {
                stage('1.11') {
                    environment {
                    	GOVERSION = '1.11.1'
                        GOROOT = "/opt/go/${env.GOVERSION}"
                        GOPATH = "/home/jenkins/go${env.GOVERSION}"
                        GO = "${env.GOROOT}/bin/go"
                        GOFMT = "${env.GOROOT}/bin/gofmt"
                        GOLINT = "${env.GOPATH}/bin/golint"
                    }
                    steps {
                        ws("${env.GOPATH}") {
                            sh "mkdir -p src/github.com/fsnotify/fsnotify"
                            sh "rsync -az ${SRC_DIR}/ src/github.com/fsnotify/fsnotify/"
                            dir("src/github.com/fsnotify/fsnotify") {
                                sh "${GO} version"
                                sh "${GO} env"
                                sh "${GO} get -t -v ./..."
                                sh "${GO} get -u golang.org/x/lint/golint"
                                sh "${GO} test ./..."
                                sh "test -z \"\$(${GOFMT} -s -l -w . | tee /dev/stderr)\""
                                sh "test -z \"\$(${GOLINT} ./... | tee /dev/stderr)\""
                                sh "${GO} vet ./..."
                            }
                        }
                    }
                }
            }
        }
    }
}
