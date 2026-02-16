🐍 PyGit — A Git Clone Built in Python

PyGit is a custom, from-scratch implementation of the Git version control system, written entirely in Python.
It is an educational project designed to deeply understand how Git works internally—its object model, staging area, commits, branches, and command-line interface.

Rather than reusing Git libraries, PyGit rebuilds Git’s core ideas from first principles to show how powerful version control emerges from a few elegant concepts.

✨ Features

PyGit implements both plumbing (low-level) and porcelain (user-facing) commands that cover most of a local, single-developer workflow.

📁 Repository Management

init — Initialize a new PyGit repository

📦 File Tracking & Staging

add — Add files or directories recursively to the staging area (index)

🕰 History & Snapshots

commit — Create a commit from staged files

log — View commit history (newest → oldest)

🌿 Branching & Navigation

branch — List branches or create a new branch

checkout — Switch branches or restore a specific commit

🔍 Inspection & Comparison

status — Show working directory and staging area status

diff — Line-by-line differences between working directory and index

cat-file — Inspect raw objects (commit, tree, blob) by hash

🧠 How PyGit Works (Git Internals Explained)

PyGit follows the same core architecture as real Git.

🗄 Object Database (.pygit/objects)

Everything is stored as an immutable object, addressed by a SHA-1 hash of its contents.

Object Types

Blob — Stores raw file contents

Tree — Represents directories (maps names → blobs/trees)

Commit — A snapshot of the project
Contains:

Root tree hash

Parent commit(s)

Author & commit message

This makes the database content-addressable and immutable.

📌 Index / Staging Area (.pygit/index)

The index is a flat file mapping:

file_path → blob_hash


It acts as a buffer between:

Working Directory → Index → Commit

🌿 References (.pygit/refs)

Branches are simple pointers to commit hashes

HEAD points to:

A branch (normal state), or

A commit (detached HEAD)

🚀 Getting Started

All commands are run via the main script.

1️⃣ Initialize a Repository
mkdir my-project
cd my-project
python /path/to/main.py init


This creates a hidden .pygit/ directory that stores all repository data.

2️⃣ Basic Workflow
# Create a file
echo "Hello, PyGit!" > README.md

# Check status (file is untracked)
python /path/to/main.py status

# Stage the file
python /path/to/main.py add README.md

# Check status again
python /path/to/main.py status

# Commit the changes
python /path/to/main.py commit -m "Initial commit"

3️⃣ Viewing Changes
# Modify a file
echo "An important update." >> README.md

# File is modified but not staged
python /path/to/main.py status

# View line-by-line differences
python /path/to/main.py diff

# Stage changes
python /path/to/main.py add README.md

# Commit update
python /path/to/main.py commit -m "Update README"

4️⃣ Branching & Checkout
# View commit history
python /path/to/main.py log

# Create a new branch
python /path/to/main.py branch feature

# List branches (* = current)
python /path/to/main.py branch

# Switch to feature branch
python /path/to/main.py checkout feature

# Make changes on feature branch
echo "A new feature" > feature.txt
python /path/to/main.py add feature.txt
python /path/to/main.py commit -m "Add new feature"

# Switch back to master
python /path/to/main.py checkout master
# feature.txt will disappear from the working directory

5️⃣ Inspecting the Object Database
# Get commit hash
python /path/to/main.py log

# Inspect a commit
python /path/to/main.py cat-file <commit-hash>

# Inspect its tree
python /path/to/main.py cat-file <tree-hash>

🛠 Future Work

Planned features:

merge — Combine histories of different branches

Conflict detection & resolution

Remote repositories (push / fetch)

Improved diff and log formatting

🎯 Why PyGit?

PyGit is ideal if you want to:

Understand Git internals

Learn about content-addressable storage

See how version control systems are built

Strengthen systems + Python skills
