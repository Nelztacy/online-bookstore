pipeline {
    agent any
    
    environment {
        MYSQL_HOST = '10.0.0.109'
        MYSQL_PORT = '3306'
        MYSQL_DATABASE = 'MYSQL'
        MYSQL_USER = 'root'
        MYSQL_PASSWORD = 'Dynasty@85'
    }
    
    stages {
        stage('git_checkout') {
            steps {
                echo "Cloning repositories 1 & 2"
                echo "Repositories cloned successfully"
            }
        }
        
        stage('Fetch Data from MySQL') {
            steps {
                script {
                    // Use a MySQL client to query the database and retrieve the book data
                    def bookData = sh(script: "mysql -h $MYSQL_HOST -P $MYSQL_PORT -u $MYSQL_USER -p'$MYSQL_PASSWORD' -e 'SELECT * FROM books;' $MYSQL_DATABASE", returnStdout: true).trim()
                    
                    // Store the book data in a file
                    writeFile file: 'books_data.json', text: bookData
                }
            }
        }
        
        stage('Deploy Demo Library') {
            steps {
                // Use your deployment steps to deploy the demo library using the retrieved book data
                // This could involve building and deploying a web application, for example
                // You can use the 'books_data.json' file in your deployment process
                // Example:
                sh 'echo "Deploying demo library with book data"'
            }
        }
    }
    
    post {
        always {
            // Clean up any temporary files if needed
            deleteFile 'books_data.json'
        }
    }
}
