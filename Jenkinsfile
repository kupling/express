pipeline {
  agent {
    node {
      label 'master'
    }

  }
  stages {
    stage('build') {
      steps {
        sh '''npm install

/home/ubuntu/node_modules/.bin/slnodejs build          \\
     --tokenfile /home/ubuntu/sltoken.txt              \\
     --buildsessionidfile /home/ubuntu/buildSessionId  \\
     --workspacepath "."                               \\
     --scm git --es6Modules

'''
      }
    }

    stage('test') {
      steps {
        sh '''/home/ubuntu/node_modules/.bin/slnodejs                \\
     mocha               \\
     --tokenfile /home/ubuntu/sltoken.txt              \\
     --buildsessionidfile /home/ubuntu/buildSessionId  \\
     --teststage "test" --useslnode2                   \\
     --                                                \\
        --require test/support/env                     \\
        --bail                                         \\
        --check-leaks test/ test/acceptance/'''
      }
    }

  }
}