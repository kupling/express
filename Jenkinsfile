pipeline {
  agent {
    node {
      label 'master'
    }

  }
  stages {
    stage('build') {
      steps {
        sh '''npm clean-install

/home/ubuntu/node_modules/.bin/slnodejs build --tokenfile /home/ubuntu/sltoken.txt --buildsessionidfile /home/ubuntu/buildSessionId --workspacepath "." --scm git --es6Modules

'''
      }
    }

    stage('test') {
      steps {
        sh '/home/ubuntu/node_modules/.bin/slnodejs /home/ubuntu/node_modules/bin/mocha --tokenfile /home/ubuntu/sltoken.txt --buildsessionidfile /home/ubuntu/buildSessionId --teststage "test" --useslnode2 -- --require test/support/env --reporter spec --bail --check-leaks test/ test/acceptance/'
      }
    }

  }
}