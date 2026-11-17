
pipeline {
    agent any

    environment {
        DEPLOY_DIR = 'C:\\jenkins_site\\'
    }

    stages {

        stage('Checkout') {
            steps {
                echo '--- Stage 1: Checkout ---'
                git branch: 'main',
                    url: 'https://github.com/shreyapatil05/DevOps_Practical.git'

                echo 'Repository checked out successfully.'
            }
        }

        stage('Validate') {
            steps {
                echo '--- Stage 2: Validate ---'

                bat '''
                    IF NOT EXIST index.html (
                        echo ERROR: index.html not found!
                        exit /b 1
                    ) ELSE (
                        echo index.html found.
                    )

                    IF NOT EXIST style.css (
                        echo ERROR: style.css not found!
                        exit /b 1
                    ) ELSE (
                        echo style.css found.
                    )

                    IF NOT EXIST Jenkinsfile (
                        echo ERROR: Jenkinsfile not found!
                        exit /b 1
                    ) ELSE (
                        echo Jenkinsfile found.
                    )

                    echo Validation passed successfully.
                '''
            }
        }

        stage('Build') {
            steps {
                echo '--- Stage 3: Build ---'

                bat '''
                    findstr /C:"Online Examination System" index.html

                    IF ERRORLEVEL 1 (
                        echo ERROR: Application title not found!
                        exit /b 1
                    )

                    findstr /C:"<link rel=" style.css

                    echo Build completed successfully.
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo '--- Stage 4: Deploy ---'

                bat '''
                    IF NOT EXIST C:\\jenkins_site (
                        mkdir C:\\jenkins_site
                        echo Created deployment directory.
                    )

                    xcopy /E /I /Y "%WORKSPACE%\\*" "C:\\jenkins_site\\"

                    echo Deployment completed successfully.
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
            echo 'Online Examination System deployed to C:\\jenkins_site\\'
        }

        failure {
            echo 'Pipeline FAILED. Please check the logs above.'
        }
    }
}
