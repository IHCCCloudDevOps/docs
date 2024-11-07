# Terraform Setup Instructions

1. Download Terraform for your operating system from hashicorp's website: https://developer.hashicorp.com/terraform/install
2. Unzip the Terraform folder and save somewhere on your computer where you'll remember (keeping the path simple can be nice, like directly under your C: drive.
3. Add Terraform to your path. If you are on Windows this will require editing your Environment Variables, on Linux/Mac you can use the terminal to add an environment variable using `export`. Google if you don't know how to do this.
4. On Windows, you'll need to restart after adding Terraform to the path.
5. Verify the installation worked by opening a console/terminal windows and typing: `terraform -v` (you should get something back like:
   ```
   Terraform v1.9.8
   on windows_386
   ```
