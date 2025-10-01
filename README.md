# Guide to Using Slurm and GitHub for Code Management

## 📌 Introduction  
This document is a practical guide for researchers, students, and developers who work in distributed computing environments using **Slurm**, a widely used workload manager in high-performance computing (HPC) clusters.  

Before running tasks on Slurm, it is crucial to maintain a clean and reproducible workflow when developing code. For this purpose, using **Git and GitHub** is highly recommended, as they allow you to manage versions, collaborate with others, and ensure that the code you run on the cluster is always up to date.  

This README first explains the basics of using Git/GitHub locally (configuration, cloning, branches, and pushing changes), and then introduces the essential commands to submit jobs with **Slurm**.  

---

## ⚙️ Git Local Setup  

1. Verify that Git is installed:  
   ```bash
   git --version



2. Clone a GitHub Repository

To work with an existing repository on GitHub:
 ```bash
  git clone https://github.com/username/repository_name.git
```

3. Move into the project directory:
 ```bash
cd repository_name
```

4. Working with Branches

Branches allow you to develop new features without affecting the main code.

List available branches and see your current branch:
```bash
git branch -a
```

Create a new branch and switch to it:

```bash
git checkout -b branch_name
```

Switch to an existing remote branch:

git checkout branch_name

5. Upload Changes to GitHub

After modifying or creating files in your project:

Check the status of your changes:
```bash
git status
```

Add changes to the staging area:

```bash
git add .
```


Commit changes with a descriptive message:

```bash
git commit -m "Brief description of changes"
```

Push your changes to the remote repository:

git push origin branch_name
