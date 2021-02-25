pipeline{
    tools{
        maven 'MAVEN_HOME'
        jdk 'JDK'
    }
    agent {label 'buildServer'}
    stages{
        stage('SCM-CHeckout'){
            steps{
               sh 'git fetch https://github.com/arvind61h/Shopeasy.git main'
            }
        }
        stage('Test-And-DockerImage'){
            steps{
                sh 'mvn clean install'
                sh 'docker ps'
                sh 'docker image prune -f'
                sh 'docker container prune -f'
                sh 'docker volume prune -f'
                sh 'docker system prune -f'
                sh 'docker build -t 92840/shop:dev .'
            }
            post{
                success{
                    archiveArtifacts artifacts: '**/*.jar, *.war', followSymlinks: false
                    //step([$class: 'JUnitResultArchiver', checksName: '', testResults: 'target/surefire-reports/*.xml'])
                }
            }
        }
        stage('Deploy on Server'){
            steps{
               sh 'docker-compose down'
            }
            
        }
    }
}