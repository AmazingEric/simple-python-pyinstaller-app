pipeline {
  agent {
    docker {
      image 'python:2-alpine'
      args 'pip install pytest'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'python -m py_compile sources/add2vals.py sources/calc.py'
      }
    }
    stage('Test') {
      steps {
        sh 'pytest --verbose --junit-xml=test-reports/results.xml sources/test_calc.py'
        junit 'test-reports/results.xml'
      }
    }
    stage('Delivery') {
      agent {
        docker {
          image 'cdrx/pyinstaller-linux:python2'
        }

      }
      steps {
        sh 'pyinstaller --onefile sources/add2vals.py'
        archiveArtifacts 'dist/add2vals'
      }
    }
  }
}