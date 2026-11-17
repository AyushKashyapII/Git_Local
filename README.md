# 🐍 PyGit — A Git Clone in Python

PyGit is a custom implementation of the Git version control system, built from scratch in Python.  
This project is an learning tool designed to explore and understand the core mechanics of Git, including its object model, staging area (index), branching, and command-line interface.

PyGit demonstrates how Git’s powerful features are built upon a few simple and elegant concepts.

---

## ✨ Features

This version of PyGit implements the core **plumbing** and **porcelain** commands that cover the majority of a local, single-developer workflow.

### 📁 Repository Management
- `init` — Initialize a new, empty PyGit repository

### 📦 File Tracking & Staging
- `add` — Add file contents to the index (staging area)  
  - Recursively adds files in directories

### 🕰 History & Snapshots
- `commit` — Create a new commit from staged files
- `log` — View commit history (newest to oldest)

### 🌿 Branching & Navigation
- `branch` — List all local branches or create a new branch
- `checkout` — Switch between branches or restore a specific commit

### 🔍 Inspection & Comparison
- `status` — Show the status of the working directory and staging area
- `diff` — Show line-by-line differences between working directory and index
- `cat-file` — Inspect any object (commit, tree, or blob) by its hash

---

## 🧠 How Git Works (The PyGit Model)

PyGit is built on the same fundamental principles as Git.

### 🗄 Object Database (`.pygit/objects`)
Everything in PyGit is stored as an **object**, identified by a unique **SHA-1 hash** computed from its contents.  
This makes the database **content-addressable** and **immutable**.

#### Object Types
- **Blob** — Stores the raw content of a file
- **Tree** — Represents a directory containing blobs and subtrees
- **Commit** — A snapshot of the project at a specific point in time  
  Includes:
  - Root tree hash
  - Parent commit(s)
  - Author and commit message

---

### 📌 Index (`.pygit/index`)
Also known as the **staging area**, the index maps file paths to blob hashes that will be included in the next commit.

