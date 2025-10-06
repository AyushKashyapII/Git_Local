PyGit - A Git Clone in Python
PyGit is a custom implementation of the Git version control system, built from scratch in Python. This project is an educational tool designed to explore and understand the core mechanics of Git, including its object model, index (staging area), branching, and command-line interface.
It demonstrates how Git's powerful features are built upon a few simple, elegant concepts.

Features
This version of PyGit implements the core "plumbing" and "porcelain" commands that cover the majority of a local, single-developer workflow.
Repository Management:
init: Initialize a new, empty PyGit repository.

File Tracking & Staging:
add: Add file contents to the index (staging area). Recursively adds files in directories.

History & Snapshots:
commit: Create a new commit to save the state of the staged files.
log: View the history of commits, from newest to oldest.

Branching & Navigation:
branch: List all local branches or create a new branch.
checkout: Switch between branches or restore the working directory to a specific commit's state.

Inspection & Comparison:
status: Show the status of the working directory and the staging area.
diff: Show line-by-line differences between the working directory and the staging area.
cat-file: Inspect any object (commit, tree, or blob) in the PyGit database by its hash.

How Git Works (The PyGit Model)
PyGit is built on the same fundamental principles as Git:
The Object Database (.pygit/objects): Everything is stored as an object (a blob, tree, or commit). Each object is identified by its unique SHA-1 hash, calculated from its content. This makes the database content-addressable and immutable.
Blob: Stores the raw content of a file.
Tree: Represents a directory. It contains a list of pointers to the blobs and other trees within it.
Commit: A snapshot of the project at a specific point in time. It contains a pointer to the root tree, parent commit(s), and metadata like the author and commit message.
The Index (.pygit/index): Also known as the staging area, the index is a flat list that maps file paths to the blob hashes of the content you want to include in the next commit. It acts as a staging ground between your working directory and your commit history.
Pointers (.pygit/refs): Branches are simply pointers—small files that contain the SHA-1 hash of a specific commit. The special HEAD pointer indicates your current location in the repository, either by pointing to a branch or a specific commit (detached HEAD).
How to Use PyGit
All commands are run from the command line via the main script.
1. Initialize a Repository
Create a new directory and run the init command. This will create the hidden .pygit directory where all the repository data is stored.
code
Bash
mkdir my-project
cd my-project
python /path/to/main.py init
2. The Basic Workflow
A typical workflow involves creating files, adding them to the staging area, and committing them.
code
Bash
# Create a new file
echo "Hello, PyGit!" > README.md

# See the status (README.md will be "untracked")
python /path/to/main.py status

# Stage the new file for the next commit
python /path/to/main.py add README.md

# See the status again (README.md will be a "new file" to be committed)
python /path/to/main.py status

# Commit the staged changes with a message
python /path/to/main.py commit -m "Initial commit"```

### 3. Viewing Changes
After making edits, you can see what has changed.

```bash
# Edit an existing file
echo "An important update." >> README.md

# See that the file is modified but not staged
python /path/to/main.py status

# See the exact line-by-line changes
python /path/to/main.py diff

# Stage the changes
python /path/to/main.py add README.md

# Commit the new version
python /path/to/main.py commit -m "Update README"```

### 4. Branching and Checking Out
Isolate work on branches and switch between them.

```bash
# See your commit history
python /path/to/main.py log

# Create a new branch called "feature"
python /path/to/main.py branch feature

# List all branches (* indicates the current branch)
python /path/to/main.py branch

# Switch to the new branch
python /path/to/main.py checkout feature

# Make some changes on the feature branch...
echo "A new feature" > feature.txt
python /path/to/main.py add feature.txt
python /path/to/main.py commit -m "Add new feature"

# Switch back to the master branch
python /path/to/main.py checkout master
# The feature.txt file will disappear from your working directory!
5. Inspecting the Database
Use cat-file to look at any object directly.
code
Bash
# Get a commit hash from the log
python /path/to/main.py log

# Inspect the commit object
python /path/to/main.py cat-file <commit-hash>

# From the commit output, get the tree hash and inspect it
python /path/to/main.py cat-file <tree-hash>
Future Work
The next major feature to be implemented is the merge command, which will allow for combining the histories of different branches.
