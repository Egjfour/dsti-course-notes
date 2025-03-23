| Course Name |      Topic      |  Professor  |     Date     | Tags |
| :---------: | :-------------: | :---------: | :----------: | :--: |
|  **MLOps**  | Version Control | Joe Sanchez | 03 mars 2025 |      |

[Professor Notes Link (Source Control)](https://github.com/adaltas/dsti-mlops-2025-spring/blob/main/03.scm/index.md)
[Professor Notes Link (Data Versioning)](https://github.com/adaltas/dsti-mlops-2025-spring/blob/main/07.data-versioning/index.md)

# Summary
*Consistency in versioning is critical in ensuring that software projects can be worked on within teams and be successfully deployed to production. For DevOps, tools like Git which provide a single source of truth for code bases are generally enough, but the additional constraints in the [[DevOps and MLOps Overview|MLOps pipeline deployment]] require additional tooling like DVC which is built on top of the git ecosystem to allow for model and data tracking as well.*

# Key Takeaways
1. Git is a distributed version control system
2. Having a central source of truth is critical in managing software teams
3. DVC supports the additional concerns of MLOps by providing a VCS solution for data and model artifacts as well

# Definitions
- Version Control System (VCS) or Source Control Management (SCM): Tools that help keep track of code with a complete history of changes
- Distributed VCS: A local database (repo) is maintained with full history alongside the remote 
	- Git
- Centralized VCS: A single central database which requires a network to inspect history 
	- Apache Subversion (SVN)
- Branch: An independent set of commits

# Additional Resources
- [Git Documentation](https://git-scm.com/doc)
- [DVC Website](https://dvc.org/)
- [DVC Install](https://dvc.org/doc/install)

# Notes
## Version Control Systems
- Tracking and managing changes to software code
- Standard and necessary in development to maintain a <mark style="background: #FFB86CA6;">single source of truth</mark>
	- Lets multiple developers work on the same codebase
- Allows for sharing work and tracking changes/authors
## Git
- Most popular VCS which is distributed, open-source, and free
- Many client tools to interact with Git
	- git CLI, Github Desktop, GitKraken, Sourcetree, Fork, and many more
- Repo hosting is available on Github, Gitlab, Bitbucket, and more
- Basic Concepts
	- The Git project:
	    - on your computer - **local repository**
	    - in a remote location - **remote repository**
	- Each set of changes to files in the history is a **commit**
	- When choosing what to commit, files are **staged**
	- Each commit has a **parent commit** (except for the first one)
	- The current commit is the **HEAD**
	- ![[Pasted image 20250323121046.png]]
- Key Commands
	- Initialize a new repo locally: `git init`
	- Clone from a remote repository for new projects: `git clone`
	- Get changes from the remote repository: `git pull`
	- Add files with changes to the local change index: `git add`
	- See the current status of all files in the working tree: `git status`
	- Create a save snapshot on the local repo of the current changes: `git commit -m "commit message"`
	- Send changes to the remote repository: `git push`
- Branching
	- Represents a line of independent development
	- These can be temporary for independent features or change requests
	- ![[Pasted image 20250323113242.png]]
	- Conflicts
		- When there are changes in the master branch that are not reflected in a branch we are trying to merge to master
		- These must be resolved manually using either rebase (preferred) or merge
			- ![[Pasted image 20250323113429.png]]
- Tagging
	- Tags are used to more easily identify commits
	- Typically this is done with the version number
	- Tags must be pushed to the remote repo the same way as commits
## Data Version Control (DVC)
- DVC is software that runs on top of git to track datasets and ML projects
- Supports building and running pipelines
- Solves the file size limit of git
	- 2GB on free git and 5GB for enterprise for Git-LFS
- Contains a Python API and uses git-style CLI commands
- Use cases for data versioning
	- **Data engineering** during data cleaning and dataset preparation
	- Test data in **software engineering** to assure the functionality of the software
	- Development and testing of **database applications**
	- Ontology versioning for **Semantic Web**
- The git repo stores metadata about the version and is included in the SCM. Then, separate `dvc push` commands save the actual data to remote data repos
	- Supports local and cloud solutions storage
	- Git tags allow us to reference prior version numbers
		- This is where consistency in [[DevOps and MLOps Overview|semantic versioning]] matters
- Python SDK
	- Using the dvc library, we can interact with versioned files directly
	- To access the most recent version, we specify the path and repo location
	```python
	import pandas as pd
	import dvc.api
	
	# Establish the path to the data file
	path='data/01_raw/wine_original.csv'
	repo='.'
	
	# Get the data from the DVC repository
	data_url = dvc.api.get_url(
	  path=path,
	  repo=repo,
	  )
	
	data = pd.read_cav(data_url)
	```
	- We can also access specific versions using their tag in git using the `rev` parameter
	```python
	data_v2_url = dvc.api.get_url(
		path=path,
		repo=repo,
		rev="v2"
	)
	data_v2 = pd.read_csv(data_v2_url)
	```