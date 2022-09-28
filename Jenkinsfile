pipeline {
  agent any
   stages {
    stage ('Build') {
      steps {
        sh 'echo "2ND ITERATION OF DEPLOYMENT #2"'
        sh '''#!/bin/bash
        python3 -m venv test3
        source test3/bin/activate
        pip install pip --upgrade
        pip install -r requirements.txt
        export FLASK_APP=application
        flask run &
        '''
     }
   }
    stage('Test 1') {
      steps{
         sh '''#!/bin/bash
         date
         whoami
         echo "HEY COW, NAME WHAT THING YOU LEARNED IN DEPLOYMENT #2...."
         echo "I LEARNED GROOOOOOOVY LOL"
         '''
      }
    }
      stage('Test 2') {
          steps {
            sh '''#!/bin/bash
            echo "This is a 2nd test script"
            echo "Date : `date`"
            echo "Hostname : `hostname`"
            '''
          }
        }
    stage ('test 3') {
      steps {
        sh '''#!/bin/bash
        source test3/bin/activate
        py.test --verbose --junit-xml test-reports/results.xml
        ''' 
      }
    
      post{
        always {
          junit 'test-reports/results.xml'
        }
      }
    }
    stage ('Deploy') {
      steps {
        sh '/var/lib/jenkins/.local/bin/eb deploy url-shortner-dev' 
      }
    }
  }
}
