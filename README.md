## Handle large files with git lfs
Large files cannot be pushed by git into repo. There is a file limit of 50 MB. File bigger than this size will either not push to the repo, or have to use `git lfs` to handle and store large files.

### Install Git LFS
Use this command:
```
git lfs --version || sudo apt-get install git-lfs
```
### Set up git lfs
1. Initialize Git LFS in your repository

```
cd /home/xps15/Web-Kafka-Reco/CUDA-examples
git lfs install
```

2. Track large file patterns with LFS
```
git lfs track "*.pt"                    # PyTorch model files
git lfs track "*.tfevents.*"            # TensorBoard event files
git lfs track "*.terraform*"            # Terraform provider files
git lfs track "Embedding-AutoEncoder/runs/**"
git lfs track "Terraform/**/*.terraform*"
```

3. Add the LFS tracking file

```
git add .gitattributes
```

4. Migrate existing large files to LFS

```
git lfs migrate import --include="*.pt,*.tfevents.*,terraform-provider-*"
```

5. Then push normally

```
git add .
git commit -m "Set up Git LFS for large files"
git push origin main
```

After Setup - Normal Git Workflow:
Once Git LFS is configured, you use Git exactly as normal:

git add .
git commit -m "your message"
git push origin main

Large files matching your LFS patterns will be automatically stored in Git LFS instead of the regular Git repository, but the commands remain the same!

Benefits:
* No size limits - Large files stored separately
* Fast cloning - Large files downloaded only when needed
* Normal workflow - Same Git commands as always
* GitHub friendly - Fully supported by GitHub

The Git LFS setup is a one-time process. After that, everything works like normal Git.


## Default Git Clone Behavior with LFS:

What happens during git clone:
* Small files: Downloaded normally (code, configs, etc.)
* LFS pointer files: Downloaded (tiny text files pointing to large files)
* Actual large files: NOT downloaded by default

What users see:

* All your code and small files work normally
* Large files appear as small "pointer files" (a few KB each)
* The repository clones much faster.

## When Large Files Are Actually Downloaded

### Automatic download:

```
git lfs pull  # Downloads all LFS files for current branch
```

### On-demand download:

```
git lfs pull --include="*.pt"  # Download only specific file types
git lfs pull path/to/specific/file.pt  # Download one specific file
```

### Configure automatic download:

```
git config lfs.fetchrecentalways true  # Always fetch LFS files
```

## Practical Example for Your Repository:
When someone clones your CUDA-examples repo:

They get immediately:
* All your .py, .cu, .md, .yaml files
* Your code structure and documentation
* Ability to run most examples

They need git lfs pull for:
* TensorBoard event files (for viewing training logs)
* Model checkpoint files (.pt files)
* Terraform provider binaries

Benefits for collaborators:
Fast clone: No waiting for 800MB+ downloads
Selective download: Only get large files they actually need
Bandwidth friendly: Don't download training artifacts unless needed


## Setup
1. Clone the repository: `git clone <repo-url>`
2. For training/TensorBoard files: `git lfs pull`
3. For specific models only: `git lfs pull --include="*.pt"`