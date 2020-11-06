import jenkins.model.Jenkins
import hudson.model.*
import groovy.json.JsonOutput
import groovy.json.JsonSlurper
import groovy.json.JsonSlurperClassic
import java.text.SimpleDateFormat

def config = [email: '${email}',
        dockerImage: '${docker_image}',
        dockerRegistryCredentials: '${dockerRegistryCredentials}']
  
def version="develop"
def tag 
def packageJSON
def triggerUser
  
pipeline {
    agent any //{
     //   label 'docker'
   // }

   // options {
    //    buildDiscarder(logRotator(numToKeepStr:'10'))
     //   disableConcurrentBuilds()
      //  sendSplunkConsoleLog()
       // timeout(time: 1, unit: 'HOURS')
    //}

    stages {
        stage('get-started') {
            steps {
                script {
                  echo 'get started'
                  tag = VersionNumber(projectStartDate: '2017-05-22', versionNumberString: 'Release.1.0.v${BUILDS_ALL_TIME}', versionPrefix: '', worstResultForIncrement: 'SUCCESS')
            }
        }
      }
        stage('perform-build') {
                steps {   
                        sh 'pwd'
                        sh 'ls -al'
                        echo "${tag}"
                }
           }
    }
    post {
      always {
        sshagent([gitCredentials]) {
            sh "git config user.email \"${email}\""
            sh "git config user.name \"${user name}\""
          //  sh "git tag -d previous_tag"
            sh "git tag -a ${tag} -m 'Adding tag'"
            sh "git push --tags"
        }
      }
   }

}
