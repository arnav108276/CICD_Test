pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/arnav108276/CICD_Test.git', branch: 'main'
            }
        }

        stage('Print Message') {
            steps {
                echo 'Hello'
            }
        }

        stage('User Input') {
            steps {
                script {
                    def userInput = input message: 'Enter a value:', parameters: [string(name: 'USER_INPUT', description: 'Type something')]
                    echo "User entered: ${userInput}"
                }
            }
        }

        stage('Print Current Directory') {
            steps {
                script {
                    def currentDir = pwd()
                    echo "Current directory: ${currentDir}"
                }
            }
        }

        stage('Change Directory to Desktop') {
            steps {
                bat 'cd "C:\Users\Arnav\OneDrive\Desktop"'
            }
        }

        stage('Compile and Run Java on Desktop') {
            steps {
                bat '''
                cd %USERPROFILE%\Desktop
                echo public class Main { public static void main(String[] args) { System.out.println("Hello from Java"); } } > Simple.java
                javac Simple.java
                java Simple
                '''
            }
        }

        stage('Create and Delete Directory') {
            steps {
                script {
                    sh 'mkdir SampleDir'
                    echo "SampleDir created"
                    sh 'rm -rf SampleDir'
                    echo "SampleDir deleted"
                }
            }
        }

        stage('Java Calculator') {
            steps {
                script {
                    def task = input message: 'Choose operation:', parameters: [choice(name: 'TASK', choices: ['add', 'sub'], description: 'Select operation')]
                    def num1 = input message: 'Enter first number:', parameters: [string(name: 'NUM1', defaultValue: '0')]
                    def num2 = input message: 'Enter second number:', parameters: [string(name: 'NUM2', defaultValue: '0')]
                    
                    bat """
                    cd %USERPROFILE%\Desktop
                    echo public class Calculator { public static void main(String[] args) { int num1 = Integer.parseInt(args[0]); int num2 = Integer.parseInt(args[1]); String task = args[2]; System.out.println(task.equals(\"add\") ? \"Result: \" + (num1 + num2) : \"Result: \" + (num1 - num2)); } } > Calculator.java
                    javac Calculator.java
                    java Calculator ${num1} ${num2} ${task}
                    """
                }
            }
        }
    }
}
