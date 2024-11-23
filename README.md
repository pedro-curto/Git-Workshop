# Git Tutorial

## Git Setup on Windows

## Step 1: Install Git for Windows
To work with SSH keys and Git, it's a good idea to have **Git for Windows** installed. Git Bash, included in Git for Windows, provides a command line interface for running Git commands.

- **Download Git for Windows**: Visit [https://gitforwindows.org/](https://gitforwindows.org/) and download the installer.
- **Install Git**: Run the installer and select the default options to complete the installation.

## Step 2: Open Git Bash
After installing Git for Windows, you need to open **Git Bash**. You can do this by typing "Git Bash" into the Windows search bar.

## Step 3: Generate an SSH Key
To generate an SSH key pair, follow these steps in Git Bash:

1. **Open Git Bash**.
2. Run the following command:

   ```sh
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
   
   - Replace `"your_email@example.com"` with the email address associated with your GitHub account (**this is important**)
   - Replace `"your_email@example.com"` with the email address associated with your GitHub account (**this is important**)
     
   - If your system doesn’t support it, you may have to use `rsa` like this:

   ```sh
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```

3. After running the command, you will see a prompt:git config --global user.email "your_email@example.com"
3. After running the command, you will see a prompt:git config --global user.email "your_email@example.com"

   ```
   Enter a file in which to save the key (/c/Users/YourName/.ssh/id_ed25519):
   ```

   - Press **Enter** to save the key to the default location (`/c/Users/YourName/.ssh`).

4. Next, it will prompt you to set a **passphrase**. You can just press **Enter** to leave it empty (I always do this).
4. Next, it will prompt you to set a **passphrase**. You can just press **Enter** to leave it empty (I always do this).

## Step 4: Start the SSH Agent
Now that you’ve generated an SSH key, you need to add it to the * *SSH agent** to manage your keys.
Now that you’ve generated an SSH key, you need to add it to the * *SSH agent** to manage your keys.

1. In Git Bash, run the following command to start the SSH agent:

   ```sh
   eval "$(ssh-agent -s)"
   ```

2. Next, add your SSH private key to the agent by running:

   ```sh
   ssh-add ~/.ssh/id_ed25519
   ```

   - If you used RSA instead, replace `id_ed25519` with `id_rsa`.

## Step 5: Add SSH Key to Your GitHub Account
Now that you have generated the SSH key and added it to the SSH agent, you need to add the public key to GitHub.

1. **Copy the SSH Key**: Run the following command to copy the SSH public key to your clipboard:

   ```sh
   clip < ~/.ssh/id_ed25519.pub
   ```

   - If you used RSA, replace `id_ed25519.pub` with `id_rsa.pub`.
   - This command copies the contents of your public key to your clipboard.

2. **Add the Key to GitHub**:
   - Go to [GitHub](https://github.com) and log in to your account.
   - In the top-right corner, click on your profile picture, and then click **Settings**.
   - In the left-hand sidebar, click **SSH and GPG keys**.
   - Click the **New SSH key** button.
   - In the **Title** field, add a descriptive name like "My Windows 10 PC".
   - Paste your SSH key into the **Key** field.
   - Click **Add SSH key**.

## Step 6: Test the SSH Connection
To confirm that your SSH key is set up correctly, you can test your connection to GitHub.

1. In Git Bash, run the following command:

   ```sh
   ssh -T git@github.com
   ```

2. You may see a message like:

   ```
   The authenticity of host 'github.com (IP ADDRESS)' can't be established.
   ```
   
   Type **yes** to continue. After that, you should see a message like:

   ```
   Hi username! You've successfully authenticated, but GitHub does not provide shell access.
   ```

   This means that your SSH key has been correctly added and is working!

## Step 7: Configuring Git with Your GitHub Account
Finally, we want to use `git config` to configure our username and email for the commits and git info
You may want to configure Git to use your GitHub account information globally on your system.

1. Set your **username**:

   ```sh
   git config --global user.name "Your Name"
   ```

2. Set your **email**:

   ```sh
   git config --global user.email "your_email@example.com"
   ```

- Now that you're ready, head on to [Practical.md](https://github.com/pedro-curto/Git-Workshop/blob/main/README.md) to start the exercises!