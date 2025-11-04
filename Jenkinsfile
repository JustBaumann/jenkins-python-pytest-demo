pipeline {
  agent any

  stages {
    stage('Prepare workspace') {
      steps {
        // Create or confirm test files exist
        writeFile file: 'requirements.txt', text: 'pytest\n'
        sh 'mkdir -p tests'
        writeFile file: 'tests/test_sample.py', text: '''
def test_addition():
    assert 1 + 1 == 2
def test_subtraction():
    assert 5 - 2 == 3
def test_failure_example():
    assert 2 * 2 == 5  # intentional fail
'''
      }
    }

    stage('Install dependencies') {
      steps {
        sh 'python3 -m venv venv'
        sh './venv/bin/pip install -r requirements.txt'
      }
    }

    stage('Run tests') {
      steps {
        sh './venv/bin/pytest --junitxml=report.xml'
      }
    }

    stage('Publish Report') {
      steps {
        junit 'report.xml'
      }
    }
  }
}
