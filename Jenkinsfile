pipeline {

     agent any
     tools {
        maven 'Maven'
     }
     stages{
          stage("build jar"){
               steps{
                   script{
                    echo 'first time building'
                    sh 'mvn package'
                   }
               }
          }
          stage("building image"){
                         steps{
                             script{
                             echo 'building docker image ...'
                             withCredentials([usernamePassword(credentialsId:'docker-hub-repo', passwordVariable:'PASS', usernameVariable: 'USER')]){
                             sh 'docker build - daymane/test_ci_cd:jma-2.0 .'
                             sh "echo $PASS | docker login -u $USER --password-stdin"
                             sh 'docker push daymane/test_ci_cd:jma-2.0'
                                 }
                              }
                         }
          }
          stage("deploy"){
                         steps{
                              echo 'first time deploying'
                         }
          }
     }

}