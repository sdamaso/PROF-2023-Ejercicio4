pipeline {
    agent any

    stages {
        stage('Backup') {
            steps {
                sh 'sqlite3 Employees.db ".mode insert" ".output backup.sql" ".dump" ".quit" | grep "^INSERT INTO" backup.sql > backup.sql'
            }
        }
        
        stage('Delete DB') {
            steps {
                sh 'rm Employees.db'
            }
        }
        
        stage('Load Schema') {
            steps {
                sh 'sqlite3 Employees.db < sqlite.sql'
            }
        }
        
        stage('Restore Data') {
            steps {
                sh 'sqlite3 Employees.db ".read backup.sql" ".quit"'
            }
        }
    }
}
