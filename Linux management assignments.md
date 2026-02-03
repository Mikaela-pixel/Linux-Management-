# Assigment 0

1. First step was to create Azure account with my HAMK credentials. I did it on the lesson so there was no problems.
2. Secont step was to request free credits for students.
3. Then we created new virtual machine. Because i folowed instructions on the lecture it was easy. I chose name for it and region, with which was a problem, but after trying few Europe regions, it finally worked on France.Also choosing subscribtion as Azure for students.Choosing x 64 as VM architecture. Then right memory as advised on lecture. I put my short name, Mika, as username. And RSA SSH Format as SSH KeyType.
4. After that going to disk settings, there we check box with Delete with VM and set network sequrity group as Basic, also allowing selected ports.
5. In Managment section we enable auto-shutdown at 7pm by our time zone.
6. After that we didnt change enything else and created VM succesfully.

# Assignment 3:
## Step 1:  Create the Tupu user using the adduser script
In this step we add new Tupu user. Then creating password and info.

>sudo adduser tupu

![alt text](<Screenshot 2026-02-03 123444.png>)

## Step 2: Create the Lupu user using the useradd command. Try to create a user profile, home directory, and user group similar to Tupu.
We were told to use following code:

>sudo useradd -m -d /home/lupu -s /bin/bash -G lupu lupu

Unfortunately it didn't worked. Giving: useradd: group 'lupu' does not exist. So i used

> sudo groupadd lupu

> sudo useradd -m -d /home/lupu -s /bin/bash -g lupu lupu

> sudo passwd lupu

This way I was able to create lupu user.

![alt text](<Screenshot 2026-02-03 124519.png>)

## Step 3: Create the Hupu system user with the login shell set to /bin/false
We were advised to use:
>sudo useradd --system --shell /bin/false hupu

I did just that

![alt text](<Screenshot 2026-02-03 124735.png>)

## Step 4: Add the users Tupu and Lupu to the sudo users.
In this step we had two options. I went with the second option of using:

>sudo usermod -aG sudo tupu

>sudo usermod -aG sudo lupu

<img width="615" height="55" alt="Screenshot 2026-02-03 125138" src="https://github.com/user-attachments/assets/3a85ae39-18c6-4743-a618-df1a8b623f80" />

## Step 5: Create a directory /opt/projekti and add both users (Tupu and Lupu) as owners. Only Tupu and Lupu should have access to list files in the directory, read, and modify them.
 I created common group for both users:
 >sudo groupadd projekti

 And added them to the group:
 >sudo usermod -aG projekti tupu

 >sudo usermod -aG projekti lupu

 Then assign group ownership:
 >sudo chown root:projekti /opt/projekti

 Then set the directory permissions:
 >sudo chmod 770 /opt/projekti

 After this, setgid bit ensures all newly created files and directories inherit the projekti group:
 >sudo chmod g+s /opt/projekti

 ![alt text](<Screenshot 2026-02-03 125741.png>)

 ## Step 6: Testing
 ### Test as Tupu:
 >su - tupu

 >cd /opt/projekti

 >touch test_tupup.txt

 >ls -l

![alt text](<Screenshot 2026-02-03 130152.png>)

### Test as lupu:
>su - lupu

>cd /opt/projekti

>echo "hello" >> test_tupu.txt 

>touch test_lupu.txt

>ls -l

![alt text](<Screenshot 2026-02-03 130328.png>)

### Test as hupu:
>su - hupu

>cd /opy/projekti

hupu is a unauthorized access so it should so access denied.

![alt text](<Screenshot 2026-02-03 130510.png>)

