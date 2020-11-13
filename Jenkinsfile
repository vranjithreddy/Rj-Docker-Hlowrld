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
def GIT_COMMIT_DESC
def timestamp = new SimpleDateFormat("yyyy-MM-dd.HH.mm.ss").format(new Date())
def gitCredentials = 'gitCredentials_id'  

//properties([pipelineTriggers([cron('H/3 * * * *')])]) //Adding CRON jobs

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
      // environment{
      //      file = fileExists "${WORKSPACE}/src/file_name"
       //}

    stages {
        stage('get-started') {
            steps {
                script {
                  echo 'get started'
                  triggerUser = getLastCommit() //Use triggerUser = getTriggerUser() to get complete trigger user info if needed
                  echo "Build triggered by " + triggerUser
                  project = "${WORKSPACE}"
                  GIT_COMMIT_DESC= sh(script:'git log --format=%B -n 1 ${GIT_COMMIT}', , returnStdout: true).trim()
                  tag = VersionNumber(projectStartDate: '2017-05-22', versionNumberString: 'Release.1.0.v${BUILDS_ALL_TIME}', versionPrefix: '', worstResultForIncrement: 'SUCCESS')
            }
        }
      }
        stage('perform-build') {
                steps {   
                        sh 'pwd'
                        sh 'ls -al'
                        echo "${tag}"
                        echo "${timestamp}"
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
