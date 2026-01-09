


┌──────────────────── ENTRYPOINT vs CMD ────────────────┬──────────────────────────── COPY vs ADD ──────────────┐
│ ENTRYPOINT                        │ CMD                 │ COPY                         │ ADD                     │
│ ───────────────────────────────── │ ───────────────── │ ─────────────────────────── │ ────────────────────── │
│ ▸ Defines the MAIN command        │ ▸ Default args or  │ ▸ Copy file from host to     │ ▸ Copy file from host  │
│   (executable) of the container  │   command           │   container                  │   or internet to       │
│                                   │                     │                              │   container            │
│ ▸ Commands are written in ENTRYPOINT │ ▸ Args usually   │ ▸ Simpler, predictable       │ ▸ Can do more complex  │
│   (WHAT to run)                   │   in CMD (HOW)     │                              │   tasks (unpack etc.) │
│ ▸ Cannot be overridden easily    │ ▸ Can be overridden │ ▸ Does NOT unpack archives  │ ▸ Can unpack archives  │
│                                   │   while running    │   automatically             │   automatically        │
│ ▸ Runs first, always executes    │ ▸ Runs after       │ ▸ Cannot fetch files from    │ ▸ Can fetch remote     │
│   when container starts           │   ENTRYPOINT       │   URLs                       │   files from internet  │
│ ▸ Only ONE ENTRYPOINT should exist │ ▸ Multiple CMDs    │ ▸ Preferred for most cases  │ ▸ Use only for remote  │
│                                   │   but last works   │                              │   or archive tasks     │
│ ▸ Not compulsory                  │ ▸ CMD is important │ ▸ Simple syntax, faster      │ ▸ Slightly slower due  │
│                                   │   (without CMD,    │   builds                     │   to extra features    │
│                                   │    container stops)│                              │                        │
│ Example:                          │ Example:           │ Example:                     │ Example:                │
│ ENTRYPOINT ["nginx"]              │ CMD ["-g","daemon off;"] │ COPY ./app /usr/src/app    │ ADD app.tar.gz /usr/src/app │
│ docker run myimage → nginx -g daemon off │ docker run myimage /bin/sh → CMD overridden │ ADD https://example.com/file.txt /usr/src/file.txt │
└────────────────────────────────────┴───────────────────────────────┴───────────────────────────┴─────────────────────┘




































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
