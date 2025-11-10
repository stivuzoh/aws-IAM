# aws-IAM
Repo on how to create IAM users and assigning roles
# 🔐 AWS IAM Step-by-Step Tutorial: Complete User & Group Management

## 📋 Overview
This tutorial walks through creating IAM policies, user groups, users, and implementing security best practices in AWS.

---

## Phase 1: 🛡️ IAM Policy Creation

### Step 1: 🏠 Access IAM Dashboard
![IAM Dashboard](Step1%20IAM%20dashboard.png)

Navigate to IAM Dashboard in AWS Console

**Check Security Recommendations:**
- Root user MFA status
- Root user access keys
- Note your Account ID: `222034742054`

### Step 2: 📋 Navigate to Policies
![Policy Dashboard](Step2%20Create%20Policy%20dashboard.png)

Go to **Access Management → Policies**  
Click **"Create policy"** button

### Step 3: ⚙️ Configure EC2 Permissions
![EC2 Actions](Step3%20EC2%20and%20All%20EC2%20actions%20selected.png)

Select EC2 service  
Choose **"All EC2 actions (ec2:*)"**

All access levels selected:
- List (198/198)
- Read (47/47)
- Write (457/457)
- Permissions management (16/16)
- Tagging (2/2)

### Step 4: 🌐 Set Resources
![All Resources](Step4%20All%20resouces%20selected.png)

Select **"All"** for resources  
> ⚠️ Note: "The all wildcard may be overly permissive"

Proceed without specific resource ARNs

### Step 5: 📝 Policy Details
![Policy Description](Step5%20Policy%20description.png)

**Policy Name:** `developers`  
**Description:** "This allows the developers to access EC2 instance!"  
Review permissions show 1 service allowed (EC2)

### Step 6: ✅ Developers Policy Created
![Policy Created](Step6%20Policy%20for%20developers%20created.png)

Successfully created developers policy  
Policy appears in **Customer managed policies** list

### Step 7: 📊 Create Analyst Policy
![Analyst Policy](Step7%20Policy%20for%20analyst%20created.png)

Create second policy named `analyst`  
**Description:** "This will allow all analyst to access S3"  
Policy for S3 access created successfully

---

## Phase 2: 👥 User Groups Setup

### Step 8: 🏗️ Create Development Team Group
![Development Group](Step8%20DevelopmentTeam%20user%20group%20created%20and%20policy%20attached.png)

**Group Name:** `Development-Team`  
Attach **developers policy**  
No users added initially

### Step 9: 📈 Create Analyst Team Group
![Analyst Group](Step9%20AnalystTeam%20user%20group%20created%20and%20policy%20attached.png)

**Group Name:** `Analyst-Team`  
Attach **analyst policy**  
No users added initially

### Step 10: ✅ Groups Created Successfully
![Groups Overview](Step10%20Development%20and%20Analyst%20user%20group%20created.png)

Both groups visible in IAM User Groups:  
- Development-Team  
- Analyst-Team

Groups show attached policies

---

## Phase 3: 👤 User Creation & Assignment

### Step 11: 👨‍💻 Create User John
![Create John](Step11%20creating%20IAM%20user%20for%20John.png)

**Username:** John  
**Console Access:** Enabled  
**Password Option:** Custom password  
**Require Password Reset:** Enabled (recommended)

### Step 12: 🔗 Add John to Development Group
![John Group Assignment](Step12%20John%20is%20added%20to%20the%20developers%20group.png)

Permissions Option: **"Add user to group"**  
Select **Development-Team** group  
John inherits EC2 permissions via group policy

### Step 13: ✅ John Created Successfully
![John Created](Step13%20user%20John%20created%20succesfully.png)

**Sign-in URL:** https://222034742054.signin.aws.amazon.com/console  
**Username:** John  
Password generated and available for download

### Step 14: 👩‍💼 Create User Mary
![Create Mary](Step14%20Creating%20IAM%20user%20Mary.png)

**Username:** Mary  
**Console Access:** Enabled  
**Password Option:** Custom password  
**Require Password Reset:** Enabled

### Step 15: 🔗 Add Mary to Analyst Group
![Mary Group Assignment](Step15%20adding%20Mary%20to%20the%20Analyst%20group.png)

Permissions Option: **"Add user to group"**  
Select **Analyst-Team** group  
Mary inherits S3 permissions via group policy

### Step 16: ✅ Mary Created Successfully
![Mary Created](Step16%20User%20Mary%20succefully%20created.png)

**Sign-in URL:** https://222034742054.signin.aws.amazon.com/console  
**Username:** Mary  
Password generated and available for download

---

## Phase 4: 🧪 Testing & Verification

### Step 17: 🔐 Login as John
![John Login](Step17%20Log%20in%20as%20John.png)

Account ID: `stiv`  
Username: John  
Enter password and click **"Sign in"**

### Step 18: 🔄 Password Reset for John
![John Password Reset](Step18%20New%20password%20for%20John.png)

System requires password reset  
Enter old password and set new one

### Step 19: 🖥️ John Launches EC2 Instance
![EC2 Launch](Step19%20Instance%20launched%20for%20IAM%20user%20John.png)

Navigate to EC2 service  
**Instance Name:** devops server  
**AMI:** Red Hat Enterprise Linux 10  
**Type:** t2.micro  
Launch instance successfully

### Step 20: ✅ Instance Running
![Instance Running](Step20%20Instance%20live%20and%20running.png)

Instance `i-0177de90b6704dafe` running  
**Public IP:** 3.134.89.228  
John successfully used EC2 permissions

### Step 21: 🚫 Access Denied for Mary
![Access Denied](Step21%20%20Acess%20denied%20to%20John%20and%20also%20Mary%20on%20Policies%20not%20assigned%20to%20them.png)

Mary receives **Access Denied** for:
- iam:ListMFADevices
- iam:ListAccessKeys
- iam:ListAccountAliases

Expected behavior — Mary only has S3 access

### Step 22: 🔐 Login as Mary
![Mary Login](step22%20Log%20in%20for%20Mary.png)

Account ID: `stiv`  
Username: Mary  
Enter password and click **"Sign in"**

### Step 23: 📦 Mary Creates S3 Bucket
![S3 Creation](Step23%20Creating%20an%20S3%20bucket.png)

Navigate to S3 service  
Click **"Create bucket"**  
S3 access confirmed

### Step 24: ✅ S3 Bucket Created
![Bucket Created](Step24%20Bucket%20created%20succesfully.png)

**Bucket Name:** `marydevops`  
**Region:** US East (Ohio)  
Successfully created — confirms S3 permissions

---

## Phase 5: 🔒 Security Hardening

### Step 25: 📱 Enable MFA for John
![MFA Selection](Step25%20Enabling%20MFA%20for%20John.png)

Navigate to **John's Security credentials**  
MFA Device Name: `Calib-MFA`  
Choose **"Authenticator app"** option

### Step 26: 📟 Scan QR Code
![QR Code](Step26%20QR%20code%20for%20John.png)

Install **Google Authenticator**, **Duo**, or **Authy**  
Scan QR code or enter secret manually

### Step 27: 🔢 Enter MFA Codes
![MFA Codes](Step27%20Code%20from%20authenticator%20imputed.png)

First Code: 611935  
Second Code: 301512  
Codes generated from authenticator app

### Step 28: ✅ MFA Enabled for John
![John MFA Enabled](Step28%20MFA%20enabled%20for%20John.png)

MFA device successfully assigned  
John now requires MFA for console access

### Step 29: ✅ MFA Enabled for Mary
![Mary MFA Enabled](Step29%20MFA%20Enabled%20for%20Mary.png)

Repeat MFA setup for Mary  
Both users now have MFA protection

### 🎯 Conclusion: Comprehensive AWS IAM Implementation

This tutorial successfully demonstrates a complete AWS IAM implementation that transforms a basic AWS account into a secure, role-based access controlled environment. The step-by-step process showcases enterprise-level identity and access management practices.

## 🎯 Key Learnings & Best Practices

### ✅ What Was Implemented:
- Role-Based Access Control (RBAC)
- Group-based permission management
- Principle of Least Privilege
- Multi-Factor Authentication (MFA)
- Password policies and rotation

### 🔒 Security Best Practices Demonstrated:
- Use groups instead of individual user policies
- Implement MFA for all users
- Follow principle of least privilege
- Use customer-managed policies
- Regular access reviews through denied attempts
