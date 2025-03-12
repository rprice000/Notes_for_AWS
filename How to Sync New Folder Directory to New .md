How to Sync New Folder Directory to New Repo in GitHub


1. Navigate to Your Local Directory
cd /path/to/your/new-directory


2. Initialize a Git Repository
git init

3. Add the Remote GitHub Repository
Go to your new repo and copy the Repo Web URL

4. Paste Web URL into Terminal
git remote add origin https://github.com/<your-github-username>/<your-repo-name>.git

4. Add Files and Make Your First Commit
Then run the following in the terminal
git add .
git commit -m "Initial commit"

5. Push to GitHub
If your GitHub repository is completely new, set the main branch and push:
git branch -M main
git push -u origin main

git push origin main
