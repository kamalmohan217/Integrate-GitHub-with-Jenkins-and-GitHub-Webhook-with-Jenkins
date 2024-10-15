# Integrate-GitHub-with-Jenkins-and-GitHub-Webhook-with-Jenkins

To integrate GitHub with Jenkins we can follow two methods

1. Using SSH Keys
2. Using Personal Access Token.

For this to achieve you must install two pluging **GitHub** and **Git**.

### 1. Integrating Jenkins with GitHub using SSH Keys.

To achieve this Go to **Manage Jenkins > System** then GitHub Servers and do the configuration as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/dc9b4e6b-b006-4dec-b11d-24ac054c7df2)
![image](https://github.com/user-attachments/assets/91ed169c-288d-4afc-84fb-3699edfee6ed)

Go to User's **Setting > SSH and GPG Keys** and provide SSH Public Key here as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/7212e1c2-3232-4cf2-a8cf-d7fb84f82244)
![image](https://github.com/user-attachments/assets/d28c539a-148d-4335-b89f-5427bb424294)

Create credential with the Option SSH Username with private key as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/705c5810-d620-4f11-b4b1-5d904ecbb0c8)
![image](https://github.com/user-attachments/assets/73855d11-82aa-4b7c-9b64-900b3e09fe40)
