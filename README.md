#  Product Concept:CloudLaunch Altschool-Month1-Assessment

This project demonstrates AWS fundamentals by setting up a **mini cloud environment** for a product called **CloudLaunch**.  

It covers:
- ✅ Hosting a static website on Amazon S3 with CloudFronts for HTTPS and   caching
- ✅ Implementing strict IAM policies for secure s3 access
- ✅ Designing a custom VPC with public, application, and database subnets

----
## 📌 Task 1 - Static Website Hosting (S3 + IAM)
-Created **3 S3 buckets**:
- 1️⃣ `cloudlaunch-site-bucket01` -Hosts the static website (public, read only)
- 2️⃣ `cloudlaunch-private-bucket01` - Private storage (IAM user can **GetObject/PutObject**)
- 3️⃣`cloudlaunch-visible-only-bucket03` - User can list but not access content

- Configured **IAM user (cloudlaunch-user)** with a custom JSON policy:
  - ✅ Read-only on site bucket
  - ✅ Get/Put on private bucket
  - ✅ No delete permissions
  - ✅ No access to contents of visible-only bucket

-Enabled **CloudFront distirbution** for HTTPS and global caching  
- 🔗 **S3 Website URL:** [Visit Site](http://cloudlaunch-site-bucket01.s3-website-eu-west-1.amazonaws.com/)  
- 🔗 **CloudFront URL:**[Visit via CloudFront](https://d3tlbzfxua5xg7.cloudfront.net/)

---
## 📌 Task 2 - VPC Design
- Created a **VPC (cloudlaunch-vpc)** with CIDR block `10.0.0.0/16`.
- Created **3 subnets**
   - Public Subnet `10.0.1.0./24`
   - App Subnet `10.0.2.0/24`
   - DB Subnet `10.0.3.0/28`

- Created and attached **Internet Gateway**.
- Configured **Route Tables**:
 -  Public subnet route table ➡️Routes to Internet Gateway (0.0.0.0/0).
 -  App and DB route tables ➡️ No internet routes (fully private).  

- Created  **Security Groups**:
  - `cloudlaunch-app-sg` ➡️ Allows HTTP (port 80) only within VPC.
  - `cloudlaunch-db-sg` ➡️ Allows MySQL (port 3306) access **from app subnet only**.

- Updated IAM policy to give **Describe** permisions for VPC components

##📄IAM Policy
[See iam-policy.json](./iam-policy. json.txt)
