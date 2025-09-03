
# 🔑 How to Access S3DF

S3DF supports three main access methods depending on your needs: terminal (SSH), remote desktop (NoMachine), and browser-based access (OnDemand). Below is a breakdown of each option:


## 1. 🖥️ SSH (Terminal Access)

If you're comfortable using a terminal, SSH is the most direct way to access S3DF.

- Use any SSH client such as:

  - macOS/Linux: Built-in terminal with ssh

  - Windows: PuTTY or Windows Terminal with OpenSSH

- Connect to the S3DF login pool using this command:

       ssh your_username@s3dflogin.slac.stanford.edu

- These login nodes are bastion hosts and only give access to your home directory.

- To use storage or run compute jobs, you’ll need to SSH again from the login node to an interactive compute node.

### ⚠️ Windows Users:
If you see an error like:

    Corrupted MAC on input or message authentication code incorrect
    
try adding this flag to your SSH command:

    ssh -m hmac-sha2-512 your_username@s3dflogin.slac.stanford.edu

## 2. 🖼️ NoMachine (Remote Desktop Access)

NoMachine offers a graphical desktop environment that works well even on slower internet connections. It’s especially useful for applications that require graphical interfaces (e.g., X11-based tools).

  - Benefits:

     - Better performance for remote graphics

     - Preserves session state if your connection drops
   
  - Connect to:

       s3dfnx.slac.stanford.edu

 - Download and install the NoMachine client for your system.

 - For detailed instructions, refer to the NoMachine access guide ().

## 3. 🌐 OnDemand (Web Portal Access)

OnDemand provides a browser-based interface for users who prefer not to use the terminal.

- Access it here:

    👉 https://s3df.slac.stanford.edu/ondemand

- Features available after login:

   - Launch a web-based terminal

   - Start Jupyter notebooks

   - Access remote desktops

   - Manage SLURM jobs and file browsing

### 💡 Ideal for beginners or anyone needing quick access without configuring SSH or desktop clients.

   ![Login Screenshot](access.png)
