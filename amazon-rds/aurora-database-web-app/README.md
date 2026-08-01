# Aurora Database with EC2 & Connecting a Web App to Aurora

This project walks through building a full-stack setup on AWS: creating an Amazon Aurora (MySQL-compatible) database cluster, launching and configuring an EC2 instance, building a simple PHP web app on that instance, and connecting the two so data entered through the web app is stored and retrievable from the Aurora database.

**What you'll build:**
- 🧱 An Amazon Aurora MySQL database
- 🌐 A web app running on an EC2 instance
- 🔗 A live connection between the web app and the database
- ✨ End-to-end data flow — enter data in the web app, see it stored in Aurora

---

## 🗂️ Table of Contents

- [What is Amazon Aurora?](#what-is-amazon-aurora)
- [Project Summary](#project-summary)
- [Part 1: Creating an Aurora Cluster](#part-1-creating-an-aurora-cluster)
- [Part 2: Creating and Connecting a Web App](#part-2-creating-and-connecting-a-web-app)
- [Testing the Web App](#testing-the-web-app)
- [Lessons Learned](#lessons-learned)

---

## What is Amazon Aurora?

Amazon Aurora is a type of relational database, useful when you need something large-scale with peak performance and high uptime. This is because Aurora databases use **clusters** (more on that below). Ordinary relational databases, like MySQL and Oracle, are more generic and cost-effective — better suited to smaller databases and less demanding workloads.

A relational database organizes data into tables — collections of rows and columns, similar to a spreadsheet.

## Project Summary

| | |
|---|---|
| **Time spent** | More than an hour on Aurora/EC2 setup, plus ~1 hour connecting the web app (including documentation) |
| **Tools used** | Amazon Aurora (MySQL), Amazon EC2, Apache, PHP, MariaDB, terminal/SSH |
| **Unexpected challenge** | The free tier no longer includes access to a MySQL database instance, which made it hard to fully follow along |
| **Highlight** | Seeing how tangible databases become once you can watch data you entered in the web app appear directly in the database |

---

## Part 1: Creating an Aurora Cluster

### Step 1 — Understand why Aurora uses clusters
Aurora databases use clusters because they're built to handle large-scale applications and heavy operations. Clustering separates database instances by the kind of work they do — **reader instances** (handle read queries) vs. **writer instances** (handle writes) — which is what gives Aurora its performance and uptime advantages over a single-instance setup.

### Step 2 — Start creating the Aurora database
Begin creating a MySQL-compatible Aurora database instance from scratch, configuring the basic settings (engine version, instance size, credentials, etc.).

### Step 3 — Pause to set up EC2 first
Halfway through, stop the database setup. Before finishing, you need an EC2 instance in place, since the database will need to connect to it.

### Step 4 — Launch an EC2 instance
Create a new EC2 instance to host the web app.

- **Create a new key pair** for the instance — this ensures a secure connection between the EC2 instance and the Aurora database later.
- **Take note of:**
  - The **Public IPv4 DNS** address and name
  - The **key pair name**

  These are needed to access the instance and confirm you have the right permissions later.

### Step 5 — Finish setting up the Aurora database
Return to the Aurora setup and complete the configuration, now that the EC2 instance exists and can be linked to the cluster.

---

## Part 2: Creating and Connecting a Web App

### Step 1 — Connect to the EC2 instance
Using terminal, secure your key pair file permissions before connecting:

```bash
chmod 400 your-key-pair.pem
```

Then SSH into the instance using its Public IPv4 DNS address.

### Step 2 — Install the required software
Update all software on the EC2 instance, then install the tools needed to run the web app:

- Apache
- PHP
- PHP Library
- MariaDB

### Step 3 — Connect the EC2 instance to Aurora
Set up the connection details between the EC2 instance and the Aurora database by editing the `dbinfo.inc` file using `nano`:

```bash
nano dbinfo.inc
```

Add the database endpoint, username, and password here so the web app can authenticate against Aurora.

<img width="867" height="343" alt="aws-databases-webapp_b7999168" src="https://github.com/user-attachments/assets/9c46e9c3-5e7c-4f92-99d6-6099de96a1ae" />
<img width="2940" height="1912" alt="aws-databases-webapp_1709b25b" src="https://github.com/user-attachments/assets/e8a53a3d-7cca-40bd-9b31-96da484fc082" />


### Step 4 — Build the web app page
Upgrade the web app by adding a `SamplePage` (a PHP file) that includes a header and a form for entering data.

<img width="2940" height="1912" alt="aws-databases-webapp_2709b25b" src="https://github.com/user-attachments/assets/6c3030dd-5a88-47cf-a751-1da503d6fed1" />

---

## Part 3: Testing the Web App

Use the **MySQL CLI** to connect to the Aurora database directly and confirm that all the data entered through the web app was successfully stored:

```bash
mysql -h <aurora-endpoint> -u <username> -p
```

Then query the relevant table to verify the entries match what was submitted through the form.

<img width="2940" height="1912" alt="aws-databases-webapp_1409z22b" src="https://github.com/user-attachments/assets/ce235913-8493-4819-bf62-0e2ab8c9ecf2" />

---

## Lessons Learned

- The AWS free tier no longer provides free access to a MySQL-compatible database, which made parts of this project harder to follow along with exactly.
- Databases feel much more tangible once you can watch data flow from a web form into a live database in real time.
- Clusters are what make Aurora suitable for large-scale, high-uptime applications — separating reader and writer instances is central to that.
