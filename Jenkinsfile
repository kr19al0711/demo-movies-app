pipeline{
    agent any
    stages{
        
        
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
