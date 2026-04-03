Hey Everyone!
I have taken up the kodekloud engineer daily challenge [100 days of Devops] and through this series, we shall slowly but steadily start solving the daily challenges.

Here’s the link to get started with the challenge: https://engineer.kodekloud.com/practice

Day #4 Task: Script Execution Permissions.
In a bid to automate backup processes, the xFusionCorp Industries sysadmin team has developed a new bash script named xfusioncorp.sh. While the script has been distributed to all necessary servers, it lacks executable permissions on <app-server> within the Stratos Datacenter.

Your task is to grant executable permissions to the /tmp/xfusioncorp.sh script on <app-server>. Additionally, ensure that all users have the capability to execute it.

Note: You can find the infrastructure details by clicking on the Details of all Users and Servers button on the top-right section of the page. Attaching the link for reference: https://kodekloudhub.github.io/kodekloud-engineer/docs/projects/nautilus#infrastructure-details

Press enter or click to view image in full size
Day #4 Task: Script Execution Permissions.
Day #4 Task: Script Execution Permissions.
Since this is pretty straightforward, let’s get on with this.

Ssh into the <app-server> given in the task:

ssh <app-server-user>@<app-server-ip>
# Enter the password when prompted.
Let’s see what’s the current permission available for the file.

ls -la /tmp/xfusioncorp.sh

# Output:
# ---------- 1 root root 40 Oct  9 16:40 /tmp/xfusioncorp.sh
As seen in the output, there’s no permission (read[r], write[w] or execute[x]) assigned for owners, groups and others for this particular file (/tmp/xfusioncorp.sh).

Write on Medium
We will need to give executable permissions for this file. To do so, you must use the chmod command. There are two ways to try this out: Via the numeric format(octal) and alphabetical(symbolic) format.

What’s the difference between the two formats?
- Numeric format overwrites all previous permissions and is very useful when you want full control of the permissions.
- Alphabetic format leaves all other permissions unchanged and is very useful for incremental changes.
So, depending on your usecase, you can make use of the right format.

#numeric or octal format.
sudo chmod 111 /tmp/xfusioncorp.sh

#Alphabetical or symbolic format.
sudo chmod a+x /tmp/xfusioncorp.sh

#Validate if the permission has changed.
ls -la /tmp/xfusioncorp.sh

# Output:
# ---x--x--x 1 root root 40 Oct  9 16:40 /tmp/xfusioncorp.sh
As observed, the executable permission is granted for all the owners, groups and others for this file.
You can give your solution for submission for this task.. But, wait… You know, how I love my validations! So, let’s validate whether all users can execute this file… After all, they did ask.. “Additionally, ensure that all users have the capability to execute it.”

So, to validate if the <app-server> user can execute the script, run the following:

sudo sh /tmp/xfusioncorp.sh

#Output will be 'Welcome to Kodekloud.'
If… Just if, let’s say, you execute this command as a normal user, you will get a permission denied error. The reason why this is happening is because as of now, only the executable permission is assigned to the file. But the shell needs to read the file contents to interpret and execute the commands inside. To do that, it needs the read permission.

sudo chmod a+x /tmp/xfusioncorp.sh
# Output:
# -r-xr-xr-x 1 root root 40 Oct  9 16:40 /tmp/xfusioncorp.sh
# Now, you should be able to run your script as a normal user.

sudo sh /tmp/xfusioncorp.sh
Remember:
chmod is not for restricting root — it's for controlling what non-root users can do.

That’s it for Day #4.
Let’s hop on to the next challenge!
See you there! Toodaloo!
