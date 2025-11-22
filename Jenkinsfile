pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/omwarkri/devops-demo.git', branch: 'main'
            }
        }

        stage('Deploy HTML to Nginx') {
            steps {
                sh '''
                    # Ensure index.html exists
                    if [ ! -f Login.html ]; then
                        echo "ERROR: Login.html not found!"
                        exit 1
                    fi

                    # Clean old files
                    sudo rm -rf /var/www/html/*

                    # Copy all files (Login.html, css, images)
                    sudo cp -r * /var/www/html/

                    # Set correct permissions
                    sudo chown -R www-data:www-data /var/www/html
                    sudo chmod -R 755 /var/www/html

                    # Restart nginx service
                    sudo systemctl restart nginx
                '''
            }
        }
    }
}
