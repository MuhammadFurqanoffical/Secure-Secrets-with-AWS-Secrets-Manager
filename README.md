# 🔐 Secure Secrets with AWS Secrets Manager

This project demonstrates how to securely manage application credentials using **AWS Secrets Manager instead of hardcoding them in source code**.

Hardcoding credentials such as API keys, database passwords, or AWS access keys is a common security mistake. If this code is pushed to a public repository, attackers could easily access these credentials and compromise cloud resources.

This project focuses on implementing **secure credential management practices, Git security workflows, and safe code sharing practices**.

---

# 🎯 Project Objective

The objective of this project was to:

- Understand the security risks of **hardcoded credentials**
- Secure sensitive credentials using **AWS Secrets Manager**
- Retrieve secrets **programmatically using Python**
- Prevent exposure of secrets when sharing code publicly
- Practice **Git security workflows including rebasing and commit cleanup**

---

# 🛠 Tools & Technologies

- AWS Secrets Manager  
- Python (boto3 SDK)  
- Git & GitHub  
- GitHub Secret Scanning  
- JSON  
- Git Rebase  

---

# ⚠️ Security Risk: Hardcoded Credentials

Initially, the application stored AWS credentials directly inside the `config.py` file:

```python
AWS_ACCESS_KEY_ID = "ACCESS_KEY"
AWS_SECRET_ACCESS_KEY = "SECRET_KEY"
AWS_REGION = "us-east-2"
```

This approach is insecure because anyone with access to the repository could steal these credentials and potentially gain access to cloud resources.

---

# 🔒 Secure Solution Using AWS Secrets Manager

Instead of storing credentials directly in the source code, the application retrieves them securely from **AWS Secrets Manager**.

```python
import boto3
import json
from botocore.exceptions import ClientError

def get_secret():
    secret_name = "aws-access-key"
    region_name = "us-east-2"

    session = boto3.session.Session()
    client = session.client(
        service_name='secretsmanager',
        region_name=region_name
    )

    try:
        response = client.get_secret_value(SecretId=secret_name)
        secret = response['SecretString']
        return secret

    except ClientError as e:
        raise e

secret_json = json.loads(get_secret())

AWS_ACCESS_KEY_ID = secret_json['AWS_ACCESS_KEY_ID']
AWS_SECRET_ACCESS_KEY = secret_json['AWS_SECRET_ACCESS_KEY']
AWS_REGION = region_name
```

This ensures that **sensitive credentials are never exposed inside the codebase**.

---

# 🧠 Key Concepts Learned

- Secure Secret Management  
- Avoiding hardcoded credentials  
- Using AWS Secrets Manager  
- Retrieving secrets programmatically with boto3  
- Understanding GitHub Secret Scanning  
- Forking vs Cloning repositories  
- Git rebasing and history rewriting  
- Merge conflict resolution  
- Removing sensitive data from Git commit history  

---

# 🔄 Git Security Workflow

During this project I practiced secure Git workflows including:

- Forking the original repository  
- Updating and committing code changes  
- Attempting to push code with credentials  
- Observing GitHub Secret Scanning blocking exposed secrets  
- Using Git interactive rebase to remove sensitive commits  
- Resolving merge conflicts  
- Verifying that credentials were removed from the repository history  

---

# 📊 Project Reflection

**Completion Time:** ~2 hours  

**Most Challenging Part:**  
Resolving merge conflicts while cleaning the commit history to remove exposed credentials.

**Most Rewarding Part:**  
Successfully securing the application by retrieving credentials from AWS Secrets Manager and ensuring the repository is safe to share publicly.

---

# 📄 Project Documentation

Full project walkthrough and explanation:

📎 `legendary-aws-security-secretsmanager.pdf`

---

# 🚀 Key Security Takeaway

Secrets should **never be stored in source code**.  
Always use a secure secrets management service such as **AWS Secrets Manager**.

---

# 👨‍💻 Author

**Muhammad Furqan**  
Cybersecurity | Cloud Security | DevSecOps  

LinkedIn:  
https://linkedin.com/in/muhammadfurqan
