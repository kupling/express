pipeline {
  agent {
    node {
      label 'master'
    }

  }
  stages {
    stage('build') {
      steps {
        sh '''export NODE_DEBUG=sl
export SL_LOG_LEVEL=debug

npm install

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
        sh '''export NODE_DEBUG=sl
export SL_LOG_LEVEL=debug

/home/ubuntu/node_modules/.bin/slnodejs                \\
     mocha                                             \\
     --tokenfile /home/ubuntu/sltoken.txt              \\
     --buildsessionidfile /home/ubuntu/buildSessionId  \\
     --teststage "test" --useslnode2                   \\
     --                                                \\
        --require test/support/env                     \\
        --reporter spec                                \\
        --bail                                         \\
        --check-leaks test/ test/acceptance/'''
      }
    }

  }
}