## Overview
This lab focused on **using Packer to create an AWS AMI** that runs **Ubuntu 24.04** with **Nginx pre-installed and configured** to serve a web page. The final goal was to create an EC2 instance from this AMI and access the hosted webpage.

---

## **Steps Followed**

### **1 Cloning the Starter Code**
The lab repository was cloned using:
```sh
git clone https://gitlab.com/cit_4640/4640-w6-lab-start-w25.git
cd 4640-w6-lab-start-w25
```

---

### **2 Editing the Packer Template (`web-front.pkr.hcl`)**
Modifications were made to the `web-front.pkr.hcl` file to:
- Use **Ubuntu 24.04** as the base image.
- Install and configure **Nginx**.
- Copy required files (`index.html`, `nginx.conf`).
- Run provisioning scripts (`install-nginx`, `setup-nginx`).

---

### **3 Formatting and Validating the Packer File**
To ensure correctness, the Packer file was **formatted and validated**:
```sh
packer fmt web-front.pkr.hcl
packer validate web-front.pkr.hcl
```
No syntax errors found.

---

### **4 Building the AMI with Packer**
The AMI was built using:
```sh
packer build web-front.pkr.hcl
```
 This process involved:
- Creating a temporary EC2 instance.
- Running provisioning scripts.
- Saving the final AMI:  
  ```
  AMI Created: ami-005724a0c2b772070
  ```

---

### **5 Launching an EC2 Instance from the AMI**
A new EC2 instance was created using **AWS Console**:
1. **AMI Selection:** `ami-005724a0c2b772070`
2. **Instance Type:** `t2.micro`
3. **Security Group:** Allowed **SSH (22)** & **HTTP (80)**
4. **Key Pair:** Used `lab4.1.pem` for SSH access.

---

### **6 SSH Into the EC2 Instance**
To connect:
```sh
ssh -i "C:\Users\Owner\.ssh\lab4.1.pem" ubuntu@ec2-34-220-174-157.us-west-2.compute.amazonaws.com
```
Successful connection.

---

### **7 Checking Nginx Status & Fixing Issues**
Inside the EC2 instance:
```sh
sudo systemctl status nginx
```
If Nginx was not running, it was started using:
```sh
sudo systemctl restart nginx
```

Additionally, the firewall and security groups were checked to allow HTTP traffic.

---

### **8 Accessing the Web Page**
The instance’s public IP was used to verify the web server:
```
http://34.220.174.157
```
The **index.html** page successfully loaded.

---

## **Final Outcome**
✔ **Packer successfully built an AWS AMI.**  
✔ **An EC2 instance was launched from the AMI.**  
✔ **Nginx was configured to serve a webpage.**  
✔ **The webpage was accessible via the public IP.**  

---

## 📸 **Screenshot**
![Screenshot 2025-02-15 174054](https://github.com/user-attachments/assets/ec3f98f2-2215-451e-a74c-8ea82d3e58fe)
