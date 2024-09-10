# Cloud Computing and DevOps

## Course Overview
This course covers key concepts and practical skills in cloud computing and DevOps, focusing on scalable, reliable, and efficient software deployment and operations. It includes cloud service models, cloud platforms, DevOps practices, monitoring, scaling, and security.

## Course Content

### **1. Introduction to Cloud Computing**

#### **Cloud Service Models**
- **IaaS (Infrastructure as a Service)**: Virtualized computing resources over the internet. Examples: AWS EC2, Azure Virtual Machines.
- **PaaS (Platform as a Service)**: Provides a platform allowing customers to develop, run, and manage applications. Examples: AWS Elastic Beanstalk, Google App Engine.
- **SaaS (Software as a Service)**: Software delivered over the internet, on a subscription basis. Examples: Google Workspace, Microsoft Office 365.

#### **Cloud Deployment Models**
- **Public Cloud**: Services offered over the public internet. Examples: AWS, Azure, Google Cloud.
- **Private Cloud**: Cloud infrastructure used exclusively by a single organization. Example: VMware Private Cloud.
- **Hybrid Cloud**: A mix of public and private clouds. Example: Azure Stack, AWS Outposts.

**Practical Exercise:**
- **Deploy a Virtual Machine** on AWS or Azure using the respective management console.

### **2. Cloud Platforms**

#### **AWS (Amazon Web Services)**
- **Compute**: EC2, Lambda
- **Storage**: S3, EBS
- **Database**: RDS, DynamoDB
- **Networking**: VPC, ELB

**Java Example (AWS SDK):**
```java
import com.amazonaws.services.s3.AmazonS3;
import com.amazonaws.services.s3.AmazonS3ClientBuilder;
import com.amazonaws.services.s3.model.PutObjectRequest;

public class S3Example {
    public static void main(String[] args) {
        AmazonS3 s3 = AmazonS3ClientBuilder.defaultClient();
        s3.putObject(new PutObjectRequest("bucket-name", "key", new File("file-path")));
        System.out.println("File uploaded to S3.");
    }
}
```

#### **Azure**
- **Compute**: Virtual Machines, Azure Functions
- **Storage**: Blob Storage, Disk Storage
- **Database**: SQL Database, Cosmos DB
- **Networking**: Virtual Network, Load Balancer

**Python Example (Azure SDK):**
```python
from azure.storage.blob import BlobServiceClient

blob_service_client = BlobServiceClient(account_url="https://<account_name>.blob.core.windows.net", credential="<your_credential>")
container_client = blob_service_client.get_container_client("my-container")
blob_client = container_client.get_blob_client("my-file.txt")

with open("local-file.txt", "rb") as data:
    blob_client.upload_blob(data)
print("File uploaded to Azure Blob Storage.")
```

#### **Google Cloud**
- **Compute**: Compute Engine, Cloud Functions
- **Storage**: Cloud Storage
- **Database**: Cloud SQL, Firestore
- **Networking**: VPC, Load Balancer

**Bash Example (Google Cloud SDK):**
```bash
gsutil cp local-file.txt gs://bucket-name/path/to/file
echo "File uploaded to Google Cloud Storage."
```

**Practical Exercise:**
- **Set Up a Cloud Storage Bucket** and upload a file using a chosen cloud provider.

### **3. DevOps Practices**

#### **Continuous Integration and Continuous Deployment (CI/CD)**
- **CI/CD Pipelines**: Automate the process of testing and deploying code. Tools: Jenkins, GitLab CI, CircleCI.

**Jenkins Pipeline Example (Jenkinsfile):**
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh './build.sh'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh './test.sh'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                sh './deploy.sh'
            }
        }
    }
}
```

#### **Infrastructure as Code (IaC)**
- **Terraform**: Tool for building, changing, and versioning infrastructure.
- **Ansible**: Configuration management tool for automating server provisioning.

**Terraform Example (main.tf):**
```hcl
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

**Ansible Example (playbook.yml):**
```yaml
- hosts: all
  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present
```

**Practical Exercise:**
- **Create a CI/CD Pipeline** using Jenkins or GitLab CI.
- **Write Terraform Code** to deploy a simple AWS infrastructure (e.g., EC2 instance).

### **4. Monitoring and Scaling**

#### **Application Performance Monitoring**
- **Tools**: Prometheus, Grafana, New Relic.

**Java Example (Prometheus):**
```java
import io.prometheus.client.Gauge;
import io.prometheus.client.exporter.HTTPServer;

public class MetricsExample {
    static final Gauge requestDuration = Gauge.build()
        .name("request_duration_seconds")
        .help("Duration of HTTP requests.")
        .register();

    public static void main(String[] args) throws Exception {
        HTTPServer server = new HTTPServer(1234);
        // Simulate some metrics
        requestDuration.set(0.5);
    }
}
```

#### **Auto-Scaling and Load Balancing**
- **AWS Auto Scaling**: Automatically adjusts the number of EC2 instances.
- **Azure Autoscale**: Automatically adjusts resources in response to demand.
- **Google Cloud Autoscaler**: Manages VM instance groups based on load.

**Practical Exercise:**
- **Configure Auto-Scaling** for an AWS EC2 instance or Azure Virtual Machine Scale Set.

#### **Cost Management and Optimization**
- **AWS Cost Explorer**: Analyze costs and usage patterns.
- **Azure Cost Management**: Monitor and control Azure spending.
- **Google Cloud Cost Management**: View and manage cloud costs.

**Practical Exercise:**
- **Set Up Cost Alerts** and **Analyze Usage Reports** on your chosen cloud platform.

### **5. Security in the Cloud**

#### **Cloud Security Best Practices**
- **IAM (Identity and Access Management)**: Manage access to cloud resources.
- **Encryption**: Encrypt data at rest and in transit.
- **Security Groups and Firewalls**: Control access to instances and services.

**Bash Example (AWS IAM Policy Creation):**
```bash
aws iam create-policy --policy-name MyPolicy --policy-document file://policy.json
```

#### **Compliance and Risk Management**
- **Compliance Standards**: GDPR, HIPAA.
- **Risk Management Tools**: AWS Config, Azure Security Center.

**Practical Exercise:**
- **Implement IAM Policies** and **Set Up Security Groups** on your chosen cloud platform.
- **Review Compliance Reports** using tools provided by the cloud provider.

---

## **Assessment**

- **Cloud Infrastructure Deployment Project**: Deploy a multi-tier application using a cloud platform.
- **CI/CD Pipeline Implementation**: Create and deploy a pipeline to automate application testing and deployment.
- **Final Exam**: Test understanding of cloud computing models, platforms, DevOps practices, and security.

## **Resources**

- **"Cloud Computing: Concepts, Technology & Architecture" by Thomas Erl**
- **"The DevOps Handbook" by Gene Kim, Patrick Debois, John Willis, Jez Humble**
