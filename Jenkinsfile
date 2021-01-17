node{ 
    stage('Git Pull'){
        git url: 'https://github.com/we45/Vulnerable-Flask-App.git'
    }   
    stage('Install tools'){
        sh '''
        pip3 install bandit safety
        '''
    }
    stage('Bandit - SAST'){
        sh '''
        bandit -f html -o bandit-result.html app.py | true
        '''
        archiveArtifacts allowEmptyArchive: true, artifacts: '**/bandit-result.html', onlyIfSuccessful: true
        publishHTML (target: [
          allowMissing: false,
          alwaysLinkToLastBuild: false,
          keepAll: true,
          reportDir: '.',
          reportFiles: 'bandit-result.html',
          reportName: "Bandit Report"
        ])
    }
    
}
