node{ 
    stage('Git Pull'){
        git url: 'https://github.com/Keeseeel/testpipe.git'
    }   
    stage('Install tools'){
        sh '''
        pip3 install bandit
        '''
    }
    stage('Bandit - SAST'){
        sh '''
        python3 -m bandit -f html -o bandit-result.html app.py | true
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
     stage('SNYK - SCA'){
        snykSecurity failOnIssues: false, severity: 'medium', snykInstallation: 'snyk', snykTokenId: '6e90237f-32ee-4061-ae51-89753d100650'
    }
    
    
    
    
}
