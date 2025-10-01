
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

Jobs are launched using a specific Python script, which handles the necessary environment setup and queues the job with Slurm directives internally.

| **Action** | **Command** | **Description** |
| :--- | :--- | :--- |
| **Submit Job** | `python3 execute_job.py --is_git` | Executes the script, queuing the job and applying version control flags. |

### 2. Arguments for `execute_job.py`

The script uses `argparse` to define the environment, resources, and execution command.

#### Slurm & Resource Variables

| Argument | Type | Default Value | Description |
| :--- | :--- | :--- | :--- |
| `--upv_alias` | `str` | "" | The **UPV username** used for Slurm job tracking. |
| `--project_name` | `str` | "" | Name used for project identification and logging. |
| `--partition_queue` | `str` | `gpuDGX` | The **queue/partition** to use. Options: `gpuServer` or `gpuDGX`. |
| `--gpus_node` | `int` | "" | **Number of GPU(s)** to be requested for the job. |

#### Script & Docker Variables

| Argument | Type | Default Value | Description |
| :--- | :--- | :--- | :--- |
| `--docker_image` | `str` | `nvcr.io/nvidia/pytorch:23.10-py3` | Name of the **Docker image** to use for the container. |
| `--docker_folder` | `str` | `""` | Folder containing a **Dockerfile** to build a custom image (if empty, uses `--docker_image`). |
| `--local_code_folder` | `str` | "" | Folder on the Slurm master where the code is located. Mapped to `/workspace/code`. |
| `--nas_data_folder` | `str` | ""| NAS folder for **datasets** (read-only). Mapped to `/workspace/data`. |
| `--nas_results_folder` | `str` |"" | NAS folder for **results**. Mapped to `/workspace/results`. |
| `--server_folder` | `str` | `""` | DGX (or server) folder to bind. Mapped to `/DGXFolder`. |
| `--command` | `str` | *Long Command* | The **command(s) to execute** inside the container (e.g., `pip install -r... && python main.py`). |

#### Git Variables

| Argument | Type | Default Value | Description |
| :--- | :--- | :--- | :--- |
| `--is_git` | `store_true` | `False` | Flag to indicate that the code should be copied using the **GIT repository**. |
| `--repo_url` | `str` | `git@github.com:CVBLAB-DEVELOP/CBIR.git` | The URL of the GIT repository to clone. |
| `--git_branch` | `str` | `develop` | The specific **branch** of the repository to download. |
| `--commit_hash` | `str` | `""` | The hash of the specific **commit version** to download (empty means the latest version). |

### 3. Monitoring and Management

Once the job is queued or running, use these commands for control and monitoring:

| **Action** | **Command** | **Description** |
| :--- | :--- | :--- |
| **View Your Jobs** | `squeue -u $USER` | Shows only your jobs that are running or pending in the queue. |
| **Attach to Docker** | `sdocker_attach --job_id <job_id>` | Attaches to the running Docker environment of a specific job (requires the job ID). |
| **Cancel Single Job** | `scancel <job_id>` | Stops and removes a specific job from the queue or execution. |
| **Cancel ALL My Jobs** | `scancel -u $USER` | Stops and removes all your jobs (running and pending) simultaneously. |

---
