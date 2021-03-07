pipeline {
    agent any

            stages {
                stage('Clone') {
                    steps {
                        git branch: 'main', url: 'https://github.com/Diogorcgb/sonar.git'
                    }
                }
                stage ('java .jar') {
                    steps {
                        sh 'javac *.java'
                        sh "jar cfe calculator.jar Calculadora2 ./*.class"
                    }   
                }
                stage('SonarQube analysis') {
                        environment { scannerHome = tool 'sonarqube' }
                    steps {
                            withSonarQubeEnv('sonarqube') {
                                    sh "${scannerHome}/bin/sonar-scanner \
                                    -D sonar.login=65aa459a2fdc71b3d8ee2e5ffc715db2acf51033 \
                                    -D sonar.projectKey=sonarqube \
                                    -D sonar.java.binaries=/var/jenkins_home/workspace/sonar \
                                    -D sonar.java.source=11 \
                                    -D sonar.host.url=http://sonarqube:9000/"
                            }
                        }
                    }

            }
}
