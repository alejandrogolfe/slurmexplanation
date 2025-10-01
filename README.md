
# 💻 Practical Guide for Code Management: Git, GitHub, and Slurm in HPC

This **README** provides an essential roadmap for **researchers, students, and developers** working in distributed computing environments. We combine the power of **Slurm** with the best practices of **version control** using **Git and GitHub**.

Our goal is to ensure a **clean, reproducible, and collaborative workflow** in High-Performance Computing (HPC) environments.

---

## 🚀 Recommended Workflow

Developing code for HPC requires discipline to ensure that the version executed on the cluster is the correct one.

1.  **Local Development:** Use Git and GitHub to version and test your code.
2.  **HPC Preparation:** Ensure your GitHub repository is up-to-date.
3.  **Cluster Execution:** Use **Slurm** to submit and manage your jobs based on your code.

---

## ⚙️ Local Git Setup and Version Control

Before submitting jobs to Slurm, your project must be under version control.

### 1. Clone an Existing Repository

To start working on a project already hosted on GitHub:

| **Action** | **Command** |
| :--- | :--- |
| **Verify Git** | `git --version` |
| **Clone Repo** | `git clone https://github.com/username/repository_name.git` |
| **Enter Directory** | `cd repository_name` |

### 2. Branch Management

**Branches** are essential for developing new features or fixing bugs without affecting the main codebase (`main`/`master`).

| **Action** | **Command** |
| :--- | :--- |
| **List Branches** | `git branch -a` |
| **Create and Switch** | `git checkout -b new_branch_name` |
| **Switch to Existing** | `git checkout branch_name` |

### 3. Upload Changes (**Push**) to GitHub

Once you've modified your code on the local branch, follow these steps to synchronize it with the remote GitHub repository:

| **Step** | **Command** | **Description** |
| :--- | :--- | :--- |
| **1. Status** | `git status` | Shows modified files. |
| **2. Staging** | `git add .` | Adds all changes to the *staging area*. |
| **3. Commit** | `git commit -m "Concise description of changes"` | **Saves** the changes with a message. |
| **4. Push** | `git push origin branch_name` | **Uploads** the *commits* to GitHub. |

---

## ⚡ Slurm: Essential Commands in HPC

**Slurm** (*Simple Linux Utility for Resource Management*) is the most common workload manager in HPC clusters.

### 1. Submit a Job

Jobs are typically defined in a shell script (`.sh`) that includes Slurm directives (lines starting with `#SBATCH`).

| **Action** | **Command** | **Description** |
| :--- | :--- | :--- |
| **Submit Job** | `sbatch my_job.sh` | Submits the script to the Slurm queue for execution. |

### 2. Monitoring and Management

Once the job is in the queue or running, you can use the following commands:

| **Action** | **Command** | **Description** |
| :--- | :--- | :--- |
| **View Your Queue** | `squeue -u $USER` | Shows only your jobs in queue or running. |
| **Cancel Job** | `scancel <job_id>` | Stops and removes a job from the queue or execution. |

### Basic Slurm Script Example (`my_job.sh`)
