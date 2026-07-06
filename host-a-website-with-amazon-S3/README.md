# Host a Static Website on Amazon S3

## 📋 Project Overview

This project demonstrates how to host a static website using **Amazon S3**. The goal was to learn the fundamentals of AWS and cloud services, and how they can be used to serve web content directly from object storage — no traditional web server required.

## 🛠️ Tools & Concepts

**Service used:** Amazon S3

**Key concepts covered:**
- S3 bucket creation and configuration
- Bucket policies
- Static website file uploads (`index.html`, image assets)
- Bucket endpoint URLs
- Access Control Lists (ACLs) and how they govern object-level access

## ⏱️ Time & Takeaways

This project took approximately **2 hours** to complete. The biggest challenge was understanding each concept as I worked through it rather than following steps blindly. The most rewarding moment was seeing the live website load successfully with no roadblocks.

---

## Step 1: Set Up an S3 Bucket

**What I did:** Created an S3 bucket to store and organize all website files.

**Time spent:** ~30 minutes — mostly spent making sure I understood *why* I was clicking each option, not just clicking through.

**Region selection:** I chose the **Ohio (us-east-2)** region since it's geographically closest to Houston, TX. Picking a nearby region helps reduce latency for end users.

**Note on naming:** S3 bucket names are **globally unique** — no two buckets across all of AWS can share the same name, similar to a domain name.

<img width="2940" height="1912" alt="aws-host-a-website-on-s3_ba6d42ad" src="https://github.com/user-attachments/assets/8fd466dd-c648-4c02-b51d-881e609f137d" />

---

## Step 2: Upload Website Files to S3

**What I did:** Uploaded the website's files into the bucket, since a bucket alone doesn't produce a website.

**Files uploaded:**
- `index.html` — defines the structure and content of the website
- `assets/` — a folder of images used throughout the site

**Why both matter:** The HTML defines the page structure, while the assets folder supplies the images referenced within it. Neither works as a complete website without the other.

<img width="2940" height="1912" alt="aws-host-a-website-on-s3_a265af88" src="https://github.com/user-attachments/assets/dbd26416-9a0e-4f19-8781-59b89a09b4eb" />

---

## Step 3: Enable Static Website Hosting

**What I did:** Configured the bucket to serve its contents as a website rather than just storing files.

**What "website hosting" means:** It's the process of exposing files through a web server so they can be rendered as web pages rather than just downloaded as raw files.

**How I enabled it:** Navigated to the **Properties** tab → **Static website hosting** panel → enabled hosting and set `index.html` as the index document.

**Access Control Lists (ACLs):** An ACL is a permission set that determines who can access a given resource (in this case, individual objects in the bucket).

<img width="2940" height="1912" alt="aws-host-a-website-on-s3_c22c54c0" src="https://github.com/user-attachments/assets/3f4d9965-6381-4926-a91c-e78014dfacd1" />

---

## Step 4: Bucket Endpoints & Fixing the 403 Error

**Bucket endpoint URL:** Once static hosting is enabled, S3 generates a public **bucket endpoint URL** — a link that anyone on the internet can use to view the hosted website.

**Initial issue:** Visiting the endpoint URL returned a **403 Forbidden** error. Even with "Block all public access" disabled at the bucket level, the individual objects inside the bucket were still private by default — public access to the bucket and public access to its objects are managed separately.

**How I fixed it:** I updated the ACLs on the objects inside the bucket to make them publicly readable. After doing this, refreshing the endpoint URL successfully displayed the website.


<img width="2940" height="1912" alt="aws-host-a-website-on-s3_5d4474f9" src="https://github.com/user-attachments/assets/b9d96972-17e3-49c6-b324-fbbc3f47abe5" />


---

## Extension: Bucket Policies

**What I did:** Added a bucket policy to prevent accidental or malicious deletion of `index.html`.

**Why bucket policies vs. ACLs:** ACLs are best for controlling public access to individual objects, while bucket policies offer more granular control over *specific actions* — defining exactly what operations are and aren't allowed on the bucket or its contents.

**Policy result:** The policy denies all principals the ability to delete `index.html`. I confirmed this worked by attempting to delete the file and receiving a **permission denied** error.

---

## 🔑 Key Learnings

- S3 can host fully functional static websites without any server management
- Public access requires configuration at **both** the bucket level and the object level
- ACLs and bucket policies serve different but complementary purposes for access control
- Small, deliberate steps (rather than rushing through the console) make it much easier to actually understand *why* each setting matters
