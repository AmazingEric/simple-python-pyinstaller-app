pipeline {
  agent {
    docker {
      image 'python:2-alpine'
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
        sh 'pip install pytest'
        sh 'pytest --verbose --junit-xml=test-reports/results.xml sources/test_calc.py'
        junit 'test-reports/results.xml'
      }
    }
  }
}