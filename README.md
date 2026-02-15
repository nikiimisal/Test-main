

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=nikiimisal&show_icons=true&theme=tokyonight&hide_border=true" height="160px" />
  <img src="https://streak-stats.demolab.com?user=nikiimisal&theme=tokyonight&hide_border=true" height="160px" />
</p>

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=nikiimisal&layout=compact&theme=tokyonight&hide_border=true" height="160px" />
</p>













                                                                                                                                                    
| Domain     | Description                                                   | Skills / Tools                                                       | Projects                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ---------- | ------------------------------------------------------------- | -------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Cloud**  | Using AWS services to build, deploy, scale & secure systems   | AWS                                                                  | - [Securing VPC](https://github.com/nikiimisal/3-tier_Architecture_Related/blob/main/VPC.md) <br> - [Movie Ticket Booking System (AWS 3-Tier Architecture)](https://github.com/nikiimisal/Project--Movie-Ticket-Booking-System-AWS-3-Tier-Architecture-/blob/main/Movie%20Ticket%20Booking%20System%20%28AWS%203-Tier%20Architecture%29.md) <br> - [Mark Your Attendance (AWS SDK 3-Tier Architecture)](https://github.com/nikiimisal/Project-Mark-Your-Attendance-3-Tier-AWS-SDK-Architecture/blob/main/README.md) <br> - [Serverless Application – Sacred Temple File Uploader (Lambda)](https://github.com/nikiimisal/project--Serverless-application--Sacred-Temple-File-Uploader--using-lambda) |
| **DevOps** | Implementing complete DevOps workflows & practical tool usage | Docker, Kubernetes, Jenkins, Terraform, Ansible, Prometheus, Grafana | - CI/CD Pipeline Setup <br> - Docker Containerization <br> - Kubernetes Deployments <br> - Terraform (IaC) <br> - Monitoring Setup                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| **SCM**    | Version control & repository management                       | GitHub, GitLab, CodeCommit                                           | - [Git & GitHub Setup](https://github.com/nikiimisal/Git-Github/tree/main) <br> - [GitLab Profile](https://gitlab.com/nikiimisal) <br> - [AWS CodeCommit]()                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

                                                                                                                                                    
                                                                                                                                                    
                                                                                                                                                    
                                                                                                                                                    
                                                                                                                                                    
                                                                                                                                                    
                                                                                                                                                    
                                                                                                                                                    
                                                                                                                                                    
                                                                                                                                                    |





- [Pod](#example-0)     - [Pod](#example-0)   - [Pod](#example-0)





| ENTRYPOINT vs CMD |  | COPY vs ADD |  |
|------------------|--|------------|--|
| **ENTRYPOINT**   | **CMD** | **COPY** | **ADD** |
| Defines the main command (executable) of the container | Default arguments or default command | Copy file from host to container | Copy file from host or internet to container |
| Commands are written in ENTRYPOINT (WHAT to run) | Arguments usually written in CMD (HOW to run) | Simpler, more predictable | Can do more complex tasks (e.g., unpack archives) |
| Cannot be overridden easily | CMD can be overridden while running the container | Does NOT unpack archives automatically | Can unpack local .tar, .tar.gz, .tar.xz automatically |
| Runs first and always executes when container starts | Runs after ENTRYPOINT (if ENTRYPOINT exists) | Cannot fetch files from URLs | Can fetch remote files from internet |
| Only ONE ENTRYPOINT should exist | Multiple CMD can exist but only the LAST CMD works | Preferred for most use-cases | Use only when you need archive extraction or remote download |
| ENTRYPOINT is NOT compulsory (optional) | CMD is IMPORTANT (without CMD container may stop immediately) | Simpler syntax, faster build | Slightly slower due to extra features |
| ENTRYPOINT gives fixed behavior | CMD gives flexible behavior | Example: `COPY ./app /usr/src/app` | Example: `ADD app.tar.gz /usr/src/app` |
| Example: `ENTRYPOINT ["nginx"]` | Example: `CMD ["-g","daemon off;"]` | Example: `COPY ./index.html /usr/share/nginx/html/` | Example: `ADD https://example.com/file.txt /usr/src/file.txt` |
| `docker run myimage` → nginx -g daemon off | `docker run myimage /bin/sh` → CMD overridden | - | - |





































<h1 align="center">🗂️ INDEX</h1>

> This repository acts as a central hub for all my **projects**, **documentation**, and **notes**.  
> You can explore everything in one place.  
> To connect with all my social profiles — [**Click Here**](https://github.com/nikiimisal/nikiimisal)

---

### 🌐 My Portfolio Website  
- **👉** [View Portfolio Repository](https://github.com/nikiimisal/Networking)

---

### 🌐 Networking  
- **GitHub Repo:** [Networking](https://github.com/nikiimisal/Networking)  
- **LinkedIn Post:** [View Post](https://github.com/nikiimisal/Networking)

---

### 💻 Basic HTML Codes  
> *Deploying a Static Website on AWS EC2: A Simple Guide*  
- **GitHub Repo:** [HTML Profile Site](https://github.com/nikiimisal/html_basic_code_myprofile)

---

### 🧱 WordPress  
- **GitHub Repo:** [WordPress Basic](https://github.com/nikiimisal/wordpress_basic)  
- **LinkedIn Post:** [View Post](https://github.com/nikiimisal/Networking)

---

### 📊 LEPM  
- **GitHub Repo:** [LEPM Project](https://github.com/nikiimisal/LAMP_ubuntu)  
- **LinkedIn Post:** [View Post](https://github.com/nikiimisal/Networking)

<h3 align="center">
  ✨ <span style="color:#00ffff; text-shadow: 0 0 5px #00ffff, 0 0 10px #00ffff, 0 0 20px #00ffff;">Project</span> ✨
</h3>

- **LEPM Project:** [LEPM Setup on Ubuntu](https://github.com/nikiimisal/LAMP_ubuntu)  
- **Advanced Project:** [LEMP with S3, CloudFront & RDS](https://github.com/nikiimisal/project-using-lapm-S3-CloudFront-RDS)

---

### 🏗️ 3-Tier Architecture (All AWS Services)

- **Main Repo:** [3-Tier Architecture Related](https://github.com/nikiimisal/3-tier_Architecture_Related)

#### 📘 Service-wise Docs
- [VPC](https://github.com/nikiimisal/3-tier_Architecture_Related/blob/main/VPC.md)  
- [VPC Peering](https://github.com/nikiimisal/3-tier_Architecture_Related/blob/main/VPC_peering.md)  
- [RDS](https://github.com/nikiimisal/3-tier_Architecture_Related/blob/main/RDS.md)  
- [NACL](https://github.com/nikiimisal/3-tier_Architecture_Related/blob/main/NACL.md)  
- [Load Balancer (LB)](https://github.com/nikiimisal/3-tier_Architecture_Related/blob/main/LOAD-BALANCER.md)  
- [Elastic Block Store (EBS)](https://github.com/nikiimisal/3-tier_Architecture_Related/blob/main/EBS.md)  
- [CloudWatch & Auto Scaling](https://github.com/nikiimisal/3-tier_Architecture_Related/blob/main/CLOUD_WATCH%20%26%20AUTOscalling.md)  
- [All Services Overview](https://github.com/nikiimisal/3-tier_Architecture_Related/blob/main/3-tier-Arc_all_servaces_include.md)

<h3 align="center">
  ✨ <span style="color:#00ffff; text-shadow: 0 0 5px #00ffff, 0 0 10px #00ffff, 0 0 20px #00ffff;">Project</span> ✨
</h3>

- **Attendance System (3-Tier AWS SDK):** [View Project](https://github.com/nikiimisal/Project-Mark-Your-Attendance-3-Tier-AWS-SDK-Architecture)  
- **Movie Ticket Booking (3-Tier AWS):** [View Project](https://github.com/nikiimisal/Project--Movie-Ticket-Booking-System-AWS-3-Tier-Architecture-)

---

### ☁️ Serverless Hosting  

<h3 align="center">
  ✨ <span style="color:#00ffff; text-shadow: 0 0 5px #00ffff, 0 0 10px #00ffff, 0 0 20px #00ffff;">Project</span> ✨
</h3>

- **Serverless Application (Sacred Temple File Uploader):**  
  [View Repository](https://github.com/nikiimisal/project--Serverless-application--Sacred-Temple-File-Uploader--using-lambda)

---

## 🧩 Upcoming Additions
> I’ll continue updating this index as I build and publish more projects.

---

## 🧠 About This Index
This repository is a **central access point** for all my GitHub projects, LinkedIn posts, and technical documentation.  
A single place to explore my **DevOps, Cloud, and Web** work.

---

<h3 align="center">⭐ If you found this helpful, consider giving it a star!</h3>
