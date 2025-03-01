pipeline {
    agent any
    stages {
        stage('Install Dependencies') {
            steps {
                sh '''
                apt-get update
                apt-get install -y python3 python3-venv python3-pip 
                python3 -m venv venv               # Create a virtual environment
                . venv/bin/activate                # Activate the virtual environment
                pip install --upgrade pip          # Upgrade pip
                pip install -r requirements.txt    # Install dependencies
                '''
            }
        }
        stage('Run Tests') {
            steps {
                sh '''
                . venv/bin/activate                # Activate the virtual environment
                pytest --maxfail=1 --disable-warnings --html=report.html
             # Generate HTML report
                '''
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'report.html', onlyIfSuccessful: false
        }
    }
}
