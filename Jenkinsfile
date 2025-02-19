pipeline {
    agent any
    
    parameters {
        string(name: 'FIRST_NUMBER', defaultValue: '0', description: 'Enter first number')
        string(name: 'SECOND_NUMBER', defaultValue: '0', description: 'Enter second number')
        choice(name: 'OPERATION', choices: ['addition', 'subtraction'], description: 'Select operation')
    }
    
    stages {
        stage('Clone Git Project') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/arnav108276/CICD_Test.git'
                echo "Git repository cloned successfully"
            }
        }
        
        stage('Print Hello') {
            steps {
                echo "Hello"
            }
        }
        
        stage('Take User Input') {
            steps {
                echo "Using parameters: FIRST_NUMBER=${params.FIRST_NUMBER}, SECOND_NUMBER=${params.SECOND_NUMBER}, OPERATION=${params.OPERATION}"
            }
        }
        
        stage('Print Current Directory') {
            steps {
                sh 'pwd'
            }
        }
        
        stage('Change to Desktop') {
            steps {
                sh '''
                    echo "Current directory before change:"
                    pwd
                    cd ~/Desktop
                    echo "Current directory after change:"
                    pwd
                '''
            }
        }
        
        stage('Create and Run Java Program') {
            steps {
                script {
                    // Create Calculator.java file
                    writeFile file: 'Calculator.java', text: '''
                        public class Calculator {
                            public static void main(String[] args) {
                                String operation = args[0];
                                int num1 = Integer.parseInt(args[1]);
                                int num2 = Integer.parseInt(args[2]);
                                
                                if (operation.equals("addition")) {
                                    System.out.println("Result: " + (num1 + num2));
                                } else if (operation.equals("subtraction")) {
                                    System.out.println("Result: " + (num1 - num2));
                                }
                            }
                        }
                    '''
                    
                    // Compile and run Java file
                    sh '''
                        javac Calculator.java
                        java Calculator ${OPERATION} ${FIRST_NUMBER} ${SECOND_NUMBER}
                    '''
                }
            }
        }
        
        stage('Directory Operations') {
            steps {
                script {
                    // Create directory
                    sh '''
                        mkdir test_directory
                        echo "Directory created"
                        ls -la
                    '''
                    
                    // Delete directory
                    sh '''
                        rm -rf test_directory
                        echo "Directory deleted"
                        ls -la
                    '''
                }
            }
        }
    }
}
