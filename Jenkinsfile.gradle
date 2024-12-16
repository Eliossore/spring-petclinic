 pipeline {
    agent any

    environment {
        DB_URL = 'jdbc:h2:~/testdb' // Change en fonction de la base de données utilisée
        DB_USER = 'root'
        DB_PASS = 'root'
    }

    stages {
        stage('Clonage du projet') {
            steps {
                echo 'Clonage du projet Spring PetClinic...'
                checkout scm
            }
        }

        stage('Construction du projet') {
            steps {
                echo 'Construction avec Gradle...'
                sh './gradlew build'
            }
        }

        stage('Mise à jour de la base de données') {
            steps {
                echo 'Application des migrations de base de données...'
                sh './gradlew flywayMigrate'
            }
        }

        stage('Exécution des tests') {
            steps {
                echo 'Exécution des tests unitaires...'
                sh './gradlew test'
            }
        }

        stage('Démarrage de l’application') {
            steps {
                echo 'Démarrage de Spring PetClinic...'
                sh './gradlew bootRun &'
            }
        }
    }

    post {
        always {
            echo 'Pipeline terminé.'
        }
    }
}
