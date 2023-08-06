To push code to Github by using SSH, we need to follow the following instructions:
1.You can change the remote URL of your repository to use SSH by running the following command: git remote set-url origin git@github.com:username/repo.git
 Make sure to replace username/repo.git with your actual repository information.
2.Generate an SSH Key (If You Haven't Already):
Open a terminal or command prompt.
Run the following command to generate an SSH key pair: ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
 Better use the email which connected to your Github account.
3.Add the SSH Key to Your GitHub Account:
  Open the public key file (usually ~/.ssh/id_rsa.pub on Linux/Mac or C:\Users\YourUser\.ssh\id_rsa.pub on Windows).
  Copy the entire contents of the file.
  Go to your GitHub account settings, then to the "SSH and GPG keys" section.
  Click "New SSH key," paste the copied key, and give it a descriptive name.
4.Test the SSH Connection:
Run the following command to test the SSH connection to GitHub: ssh -T git@github.com
You should see a message like "Hi username! You've successfully authenticated..."
5.Push Your Code:
After setting the remote URL to use SSH and adding your SSH key to GitHub, you can push your code as you normally would: git push origin master
  Replace master with the appropriate branch name if needed.

Please note that:
1.Repository Path: You need to execute the git remote set-url command within the local directory of the Git repository you want to configure. It won't work if you run it from a directory that is not a Git repository.
2.Correct URL: Make sure to use the correct SSH URL for the repository. You can find this URL on the GitHub page for the repository, under the "Code" button. Choose the "SSH" option to see the SSH URL.
