# Integrate-GitHub-with-Jenkins-and-GitHub-Webhook-with-Jenkins

To integrate GitHub with Jenkins we can follow two methods

1. Using SSH Keys
2. Using Personal Access Token.

For this to achieve you must install two pluging **GitHub** and **Git**.

### 1. Integrating GitHub with Jenkins using SSH Keys.

To achieve this Go to **Manage Jenkins > System** then GitHub Servers and do the configuration as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/dc9b4e6b-b006-4dec-b11d-24ac054c7df2)
![image](https://github.com/user-attachments/assets/2b77b623-37c9-4f64-bd41-0b15ba764b02)

Go to User's **Setting > SSH and GPG Keys** and provide SSH Public Key here as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/7212e1c2-3232-4cf2-a8cf-d7fb84f82244)
![image](https://github.com/user-attachments/assets/d28c539a-148d-4335-b89f-5427bb424294)

Create credential with the Option SSH Username with private key as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/02525c1d-920f-44a0-81e5-053d6bd9a577)
![image](https://github.com/user-attachments/assets/7ee1580d-b0ac-4726-85b6-137c5afae495)

![image](https://github.com/user-attachments/assets/02156edc-4fb3-4518-ba3b-8c41278f1971)

Here I am using SSH Keys for Authentication and the Git Repo URL will be as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/8362e243-2f66-4f35-8ff8-d91e2eecde70)

The SSH Private and Public Keys which I had used was present on the Jenkins Slave Node as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/0319b09b-88bd-4a75-a9a5-5c64f3626706)

The Jenkins Job has been created as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/93c9f2e2-9e1e-49ea-9959-11eb2745fd87)
![image](https://github.com/user-attachments/assets/a539fa0a-6dee-493f-8fa7-0ef485809631)

The declarative pipeline is as written below.

```
pipeline{
    agent{
        node{
            label "Slave-1"
            customWorkspace "/home/jenkins/demo"
        }
    }
    parameters { 
        string(name: 'COMMIT_ID', defaultValue: '', description: 'Provide Commit ID') 
    }
    stages{
        stage("clone-code"){
            steps{
                cleanWs()
                checkout scmGit(branches: [[name: "${COMMIT_ID}"]], extensions: [], userRemoteConfigs: [[credentialsId: 'github-cred', url: 'git@github.com:singhritesh85/hello-world2.git']])
            }
        }
    }
}
```

Finally while running the Jenkins Job I provided Commit ID and Jenkins Job ran successfully.

### 2. Integrating GitHub with Jenkins Using Personal Access Token.

Created Jenkins credential with username and password as shown in the screenshot attached below. For username provide the username for GitHub and Password as Personal Access Token (PAT).

![image](https://github.com/user-attachments/assets/5b26cc4d-bd06-4a98-90c1-e0b1c299c58b)

Create Jenkins Job as shown in the screenshot attached below with webhook.

![image](https://github.com/user-attachments/assets/349d08b6-38e4-40a4-8359-1eb502a2076b)

```
pipeline{
    agent{
        node{
            label "Slave-1"
            customWorkspace "/home/jenkins/demo"
        }
    }
    stages{
        stage("clone-code"){
            steps{
                cleanWs()
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/singhritesh85/hello-world2.git']])
            }
        }
    }
}
```

Configuration in GitHub Repository setting is as shown in the screenshot attached below. 

![image](https://github.com/user-attachments/assets/17f2087a-ccf8-40e3-a61f-fe6c7e7df2a8)
![image](https://github.com/user-attachments/assets/0e2f70fa-bedb-4c01-96b6-339213324bbf)
![image](https://github.com/user-attachments/assets/29fa6428-e877-4611-bc0d-5a0c8536f922)

I did some changes in Dockerfile and webhook triggered as shown in the screenshot attached below and Jenkins Job ran successfully. 

![image](https://github.com/user-attachments/assets/6ecb5b60-a9d8-4b03-b725-0915ba2d4c9e)
![image](https://github.com/user-attachments/assets/7652a152-d010-456e-bc4d-a48fbfd9fc64)

The source code is present in GitHub Private Repo as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/c4f24b4a-2dcc-4c32-9123-5f289c246470)
