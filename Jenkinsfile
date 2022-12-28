pipeline {
  agent {
    kubernetes {
      inheritFrom 'jenkins-jenkins-agent'
      }
  }
    environment{
      TAG= '@Smoke'
      TESTTYPE= 'parallel'
      BROWSERTYPE= 'chromeHeadless'
      LANG= '@EN'
    }

    stages {      
          stage('Valores de las variables') {
            steps {
               sh 'echo "Valores de las variables"'
               sh 'echo "TAG= $TAG"'
               sh 'echo "TESTTYPE= $TESTTYPE"'
               sh 'echo "BROWSERTYPE= $BROWSERTYPE"'
               sh 'echo "LANG= $LANG"'
            }
        }

          stage('realizando pruebas') { 
            agent {
              kubernetes {
                yaml '''
                    spec:
                    containers:
                    - name: lippia
                      image: crowdar/lippia:3.2.1.1
                    '''
            }
            }
            steps {
             sh 'ls -a'
             sh 'mvn clean test -P$TESTTYPE -P$BROWSERTYPE -Dcucumber.tags="--tags $TAG"'
            }
          }
    
        }
    }  


