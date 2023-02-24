pipeline {
    agent any
    tools {
        maven 'MAVEN'
    }
    stages{
        stage('GitHub-Webhook'){
            steps{
                script{
                    properties([pipelineTriggers([githubPush()])])
                }
            }
        }
        stage('Git-clone'){
            steps{
                git branch: 'FIRST', url: 'https://github.com/chaithanya1812/test10-Ansible-DockerSwarm.git'
            }
        }
        stage('Maven-Build'){
            steps{
                sh 'mvn clean package'
            }
        }
        /*
        stage('SonarqubeReport'){
            steps{
                sh 'mvn sonar:sonar'
            }
        }
        */
        stage('Nexus-Artifact'){
            steps{
                sh 'mvn deploy'
            }
        }
        stage('Docker-login'){
            steps{
            withCredentials([string(credentialsId: 'ddockerloginn', variable: 'Dockerlogin')]) {
            sh 'docker login -u chaitu1812 --password $Dockerlogin ||true'
            }
          }
        }
        stage('Docker-build & push'){
          steps{
              sh 'docker build -t chaitu1812/movieapp .'
              sh 'docker push chaitu1812/movieapp'
              sh 'docker rmi chaitu1812/movieapp'
          }
        }
        stage('AnsibleMaster to ApacheTomcat deploy'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'AnsibleMaster', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ansible-playbook tomcatdeploy.yaml ', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '/target/', sourceFiles: '**/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        stage('Deploy into Docker-swarm'){
            steps{
                script{
                    def movieappservice = "docker service create --name movieapp --replicas 5 -p 8082:8080 chaitu1812/movieapp"
                    def removeservice = "docker service rm movieapp"
                    sshagent(['dockerswarm']) {
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@13.232.1.17 $removeservice || true"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@13.232.1.17 $movieappservice"
                    }
                }
           }
        }
        
    }
}
