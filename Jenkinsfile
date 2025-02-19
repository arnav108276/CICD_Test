pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/arnav108276/CICD_Test.git', branch: 'main'
            }
        }

        stage('Print Hello') {
            steps {
                echo 'Hello'
            }
        }

        stage('User Input') {
            steps {
                script {
                    def userInput = input message: 'Enter a value:', parameters: [string(defaultValue: '', description: 'Type something', name: 'USER_INPUT')]
                    echo "User entered: ${userInput}"
                }
            }
        }

        stage('Current Directory') {
            steps {
                script {
                    def currentDir = sh(script: 'pwd', returnStdout: true).trim()
                    echo "Current directory: ${currentDir}"
                }
            }
        }

        stage('Change Directory to Desktop') {
            steps {
                script {
                    DESKTOP_DIR = "C:\Users\Arnav\OneDrive\Desktop\lab7-jenkins"
                    sh "cd ${DESKTOP_DIR} && echo 'Changed directory to Desktop'"
                }
            }
        }

        stage('Compile and Run Java File') {
            steps {
                script {
                    sh '''
                    echo 'public class MyProgram { public static void main(String[] args) { System.out.println("Hello from Java!"); } }' > MyProgram.java
                    javac MyProgram.java
                    java MyProgram
                    '''
                }
            }
        }

        stage('Delete Directory') {
            steps {
                script {
                    def dirExists = sh(script: 'if [ -d "SampleDir" ]; then echo "exists"; else echo "not exists"; fi', returnStdout: true).trim()
                    if (dirExists == "exists") {
                        sh 'rm -rf SampleDir'
                        echo "Deleted directory from project folder"
                    } else {
                        echo "Already deleted"
                    }
                }
            }
        }
        stage('Get User Input for Java Program') {
            steps {
                script {
                    env.TASK = input message: 'Choose operation:', parameters: [choice(choices: ['add', 'sub'], description: 'Select operation', name: 'TASK')]
                    env.NUM1 = input message: 'Enter first integer:', parameters: [string(defaultValue: '0', description: 'First number', name: 'NUM1')]
                    env.NUM2 = input message: 'Enter second integer:', parameters: [string(defaultValue: '0', description: 'Second number', name: 'NUM2')]
                }
            }
        }

        stage('Compile and Run Addition & Subtraction Program') {
            steps {
                script {
                    sh '''
                    echo 'public class Calculator {
                        public static void main(String[] args) {
                            if (args.length != 3) {
                                System.out.println("Usage: java Calculator <add/sub> <num1> <num2>");
                                return;
                            }
                            String task = args[0];
                            int num1 = Integer.parseInt(args[1]);
                            int num2 = Integer.parseInt(args[2]);

                            if ("add".equalsIgnoreCase(task)) {
                                System.out.println("Addition result: " + (num1 + num2));
                            } else if ("sub".equalsIgnoreCase(task)) {
                                System.out.println("Subtraction result: " + (num1 - num2));
                            } else {
                                System.out.println("Invalid task. Use 'add' or 'sub'.");
                            }
                        }
                    }' > Calculator.java

                    javac Calculator.java
                    java Calculator ${TASK} ${NUM1} ${NUM2}
                    '''
                }
            }
        }
    }
}
