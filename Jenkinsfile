pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/my-org/my-repo.git'
            }
        }
        
        stage('Terraform Init') {
            steps {
                terraformInit(
                    backendConfigurations: [
                        [key: "bucket", value: "my-terraform-state-bucket"],
                        [key: "region", value: "us-west-2"],
                        [key: "dynamodb_table", value: "my-terraform-state-lock-table"]
                    ],
                    extraArgs: [
                        "-var",
                        "region=us-west-2",
                        "-var",
                        "vpc_cidr=10.0.0.0/16"
                    ],
                    version: "1.0.4"
                )
            }
        }
        
        stage('Terraform Plan') {
            steps {
                terraformPlan(
                    extraArgs: [
                        "-var",
                        "region=us-west-2",
                        "-var",
                        "vpc_cidr=10.0.0.0/16"
                    ]
                )
            }
        }
        
        stage('Terraform Apply') {
            steps {
                terraformApply(
                    extraArgs: [
                        "-var",
                        "region=us-west-2",
                        "-var",
                        "vpc_cidr=10.0.0.0/16"
                    ]
                )
            }
        }
    }
}
