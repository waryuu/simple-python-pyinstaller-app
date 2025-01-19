node {
    stage('Git Checkout') {
        docker.image('python:2-alpine').inside {
            git url: "https://github.com/waryuu/simple-python-pyinstaller-app/", branch:"master"
        }
    }
    stage('Build') {
        docker.image('python:2-alpine').inside {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
    }
    stage('Test') {
        docker.image('qnib/pytest').inside {
            sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
        }
        junit 'test-reports/results.xml'
    }
        stage('Deploy') {
            docker.image('cdrx/pyinstaller-linux:python2').inside {
                sh 'pyinstaller --onefile sources/add2vals.py'
                sh 'sleep 60'
            }
        }
    }