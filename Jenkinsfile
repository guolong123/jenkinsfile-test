pipeline {
  agent {
    label 'master'
  }
  stages {
    stage('build') {
      parallel {
        stage('echo-env') {
          agent {
            docker {
              image 'aslan-spock-register.qiniu.io/pandora/node-jdk:n12j11'
              reuseNode true
            }

          }
          steps {
            sh(label: 'echo env', script: "echo ${env.ENV1}")
            sh(label: 'echo env', script: "echo ${env.ENV2}")
          }
        }

        stage('echo-parameter') {
          agent {
            docker {
              image 'aslan-spock-register.qiniu.io/pandora/node-jdk:n12j11'
              reuseNode true
            }

          }
          steps {
            sh(label: 'echo parameters', script: "echo ${bool}")
            sh(label: 'echo parameters', script: "echo ${choice}")
            sh(label: 'echo parameters', script: "echo ${credential}")
            sh(label: 'echo parameters', script: "echo ${password}")
            sh(label: 'echo parameters', script: "echo ${string}")
            sh(label: 'echo parameters', script: "echo \"${text}\"")
          }
        }

      }
    }

    stage('test') {
      steps {
        echo 'test'
      }
    }

  }
  environment {
    ENV1 = '1'
    ENV2 = '2'
  }
  post {
    always {
      echo 'end'
    }

  }
  options {
    buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '14', numToKeepStr: '30'))
  }
  parameters {
    booleanParam(defaultValue: true, description: 'bool parameters', name: 'bool')
    choice(choices: ['a', 'b', 'c'], description: 'choice parameters', name: 'choice')
    credentials(credentialType: 'com.cloudbees.plugins.credentials.common.StandardCredentials', defaultValue: '6e537068-2b11-41d8-87ad-0f4ffde6b763', name: 'credential', required: false)
    file(description: 'file parameters', name: 'file')
    password(defaultValue: '123456', description: 'password parameters', name: 'password')
    run(description: 'run parameters', filter: 'ALL', name: 'run', projectName: 'phoenix-build')
    string(defaultValue: 'default value', description: 'string parameters', name: 'string')
    text(defaultValue: '''default 
value
...''', description: 'text parameters', name: 'text')
  }
}