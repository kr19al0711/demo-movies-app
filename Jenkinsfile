pipeline{
    agent any
    stages{
        
        stage("Checkout scm"){
            
            steps{
                cleanWs()
            checkout scmGit(branches: [[name: '*/feature/enabling-cicd']], extensions: [], userRemoteConfigs: [[credentialsId: '275f2b2e-01fd-486e-9682-d713895e7769', url: 'https://github.com/kr19al0711/demo-movies-app.git']])
            
            }
            
        }
        stage("Check npm and node installation"){
            steps{
            
            nodejs(cacheLocationStrategy: workspace(), nodeJSInstallationName: 'default') {
                sh '''
                    ls -la
                    npm --version
                    node -v
                '''
                }
            }
        }
        stage("Build Frontend"){
            steps{
                nodejs(cacheLocationStrategy: workspace(), nodeJSInstallationName: 'default') {
                sh '''
                    ls -la
                    cd client
                    npm install
                    npm run build 
                    
                    ls -la
                '''
            }

            }
        }
        stage("Check docker version"){
            steps{
                sh ''' docker --version '''
            }
        }
        
        stage("Dockerize movies client"){
            steps{
                sh '''
                    cd client
                    docker build --tag test .
                '''
            }
        }
    }
}
