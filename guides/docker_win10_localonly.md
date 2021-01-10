---
title: Creating BC Containers for Local Use
subtitle: Generating Docker Containers for Docker Desktop on a Windows 10 system with local (host) access only
layout: "page"
icon: fa-desktop
order: 11
hide: true
---

* auto-gen TOC:
{:toc}

#### First Note

*This guide will have the assumption that you have already installed Docker Desktop, have it running on your computer and have it switched to Windows Containers.*

## Before you begin

We will need to prepare your PowerShell environment before we get started.  To do this, you will need to open "Windows PowerShell ISE" as an Elevated user ("Run as Administrator").  This is done by doing the following:

1.  Open your START Menu
2.  Locate Windows PowerShell ISE
3.  Right Click on the program and then Click "More"-\> "Run As Administrator"

Once Windows PowerShell ISE is started, it will allow us to prepare the environment to use with BC Containers by running the following set of scripts in order.

Powershell Commands to run:
```
Install-Module PowerShellGet -Force -AllowClobber
Install-Module BcContainerHelper
Import-Module BcContainerHelper
```

## Time to get started

The first step of getting a BC docker container set up, is to run the first PowerShell command.
*If you've closed the previous session of Windows PowerShell ISE, please repeat step 1-3 in the "Before you Begin" section.*

PowerShell Command to run:
```
New-BcContainerWizard
```
This will create a separate PowerShell window with the setup guide of a new BC Container for Docker.

## BC Container Wizard - Step by Step

---
### 1. Accept Eula

As you've started the "BcContainerWizard", you will be first asked to accept the Microsoft End User License Agreement.
> ![](/assets/images/local10/image1.png)

If you agree to the Microsoft EULA, simply accept by typing in "**Y**" for "Yes" at the end of this section, followed by submitting it with the **ENTER** Key.

---
### 2. Local Container or Azure VM

Once the Microsoft EULA has been accepted, you will be asked where the container is supposed to be stored.
> ![](/assets/images/local10/image2.png)

Since this guide will focus on a Local 'On-Prem' setup, we will take option "**a**" for "Local docker container" to continue with this setup by simply typing "**a**" at the end of this section, followed by submitting it with the **ENTER** key.


---
### 3. Authentication

As the next step of this BC Docker Wizard, we face the option on how we will authenticate our login into the Docker Container.
> ![](/assets/images/local10/image3.png)

The choice here will vary depending on how you wish for it to be setup, where the options are the following:
a.  Username/Password authentication -- Once this Wizard is done and you launch the newly created script you will be met with a Windows PowerShell credential request where you set up the administrative login for the BC Container.

> ![](/assets/images/local10/image4.png)

b.  Username/Password authentication (admin with predefined password -- P\@ssw0rd) - This option will create an Administrative login with the login credentials: Admin -- P\@ssw0rd
c.  Username/Password Authentication (admin with random password -- xxxxxxxx) - This option will create an Administrative login with the login User **Admin**and generate a random password, where the generated password will be seen at the end of the option name (ex. The random password made in this guide was "Puri7313")
d.  Windows Authentication - This option will use your pre-existing username on your machine, this will include the domain you are part of, if you are part of one.

---
### 4. Container Name
The next step of this wizard will let you choose the name of your BC Container.
> ![](/assets/images/local10/image5.png)

We have chosen our own name "SpareBrainedIdeasAB" in this example and this name will reflect the name of the container inside Docker, as seen in the picture bellow.
> ![](/assets/images/local10/image6.png)

Feel free to pick whatever name you deem fit for your use, followed by submitting it with the **ENTER** key.

---
### 5. Version
At the next step of this wizard, we get the option of picking which instance of Business Central you wish to install.
> ![](/assets/images/local10/image7.png)

The options given here are quite straight forward where each option will do the following:
**a** & **b**. Latest Business Central Sandbox / OnPrem -- This option will move forward to the next step.
**c** & **d**. Insider Business Central Sandbox for Next Major / Minor release -- Requires an Insider SAS token supplied by Microsoft to be applied at the next step to continue with this option, as seen in the picture below:
> ![](/assets/images/local10/image8.png)

**e** & **f**. Specific Business Central Sandbox/OnPrem build -- This option is for when you need a specific build and the wizard requires you to follow up with the full version number after you've picked this option, as seen if the picture bellow:
> ![](/assets/images/local10/image9.png)

**g**, **h** & **i**. Specific NAV 20xx version -- requires you to supply the CU number of the build you wish to use. ('0' is considered as "RTM" and leaving it blank will default to the latest version.) See picture bellow:
> ![](/assets/images/local10/image10.png)

For the purpose of this guide, we will pick option "**b**" for "Latest Business Central OnPrem", followed by submitting it with the **ENTER** key.

---
### 6. Country
Now we are asked to provide what country version we wish to use.
> ![](/assets/images/local10/image11.png)

We will stick to the default for this guide by either writing "**w1**" (Worldwide, the 'foundation' version) or simply leaving it blank, followed by submitting it with the **ENTER**
key.


---
### 7. Test Toolkit
Next part will be the option to chose if we need the test toolkit to beinstalled.
> ![](/assets/images/local10/image12.png)

The Test Toolkit is primarily used for developers or consultants who will be running Testing tools against customizations, and will covered in this guide.

We will pick the default option "**d**" for "No Test Toolkit needed", followed by submitting it with the **ENTER** key.

---
### 8. AL Base App Development
The next step provided will give you the option to enable "AL Base App Development"
> ![](/assets/images/local10/image13.png)

This option is rarely used and for the users of this guide it will **Not** be applied, meaning we will reply to this with the default option "**N**" for "No", followed by submitting it with the **ENTER** key.

---
### 9. AL Language Extension
Following step, AL Language Extension, is not as crucial as previous options.
> ![](/assets/images/local10/image14.png)

Since we have picked the latest OnPrem build of Business Central for this guide we are in no need of installing a newer version of the AL Language Extension, we will pick the default option "**N**" for "No" followed by submitting it with the **ENTER** key.

---
### 10. License
Next step, what license to use for this installation
> ![](/assets/images/local10/image15.png)

At this step, you have the option to either supply the local location or URL for your license file, or you can leave this blank to use the default Cronus Demo License.
1.  If you wish to provide the local license file, you will need to submit the full file path.
2.  If you wish to use a secure direct download URL, see the given link provided in the wizard: <https://freddysblog.com/2017/02/26/create-a-secure-url-to-a-file/>
We will leave this option blank and use the default Cronus Demo License followed by submitting it with the **ENTER** key.

---
### 11. Database
At this step we will pick the location of the database
> ![](/assets/images/local10/image16.png)

The choice will vary depending on a few parameters:
a.  This option will use the default instance and install the selected Database version(In this guide we will be using the Cronus Demo Database) on SQLEXPRESS within the container we are currently setting up.
b.  This option is used if you already have a database backup and wish to restore it to the container we are currently setting up. (Note that this requires the version of the Database has to match the BC/NAV version provided earlier in this wizard.)  You will need to provide the full path and filename of the database backup once you've selected this option.
> ![](/assets/images/local10/image17.png)

c.  This option is used for the instance where the database is already located on a separate database server, this option requires you to modify the connection string to the proper Database location as well as user authentication, see the wizard for the correct format needed (as seen in picture bellow).
> ![](/assets/images/local10/image18.png)

We will be installing our version of Cronus Demo Database within the given container, i.e. we will pick the default option "**a**" followed by submitting it with the **ENTER** key.

---
### 12. Multitenant
This step will provide the option of using either a "singletenant" or a "multitenant".
> ![](/assets/images/local10/image19.png)

Per standard Cloud instances are Multitenant, while On-Prem installations vary. If this installation is to test a Cloud extension locally, you should select Multitenant to this installation.
We will continue this guide with the default, i.e "Singletenant" by either typing "**N**" for "No" or leaving it blank, followed by submitting it with the **ENTER** key.

---
### 13. DNS
Next we will choose the option for the DNS.
> ![](/assets/images/local10/image20.png)

The option here will reflect how the docker containers resolve their DNS queries.
a.  This option will default to the DNS configured in the Docker Daemon
b.  This option will set the DNS to Googles Public DNS, i.e 8.8.8.8
c.  This option will use the DNS that is in use on the HOST Machine.

We recommend either picking option "**b**" or "**c**" where we will be able to modify the entry later before running the finished script.

We will pick option "**b**" for the Google Public DNS followed by submitting it with the **ENTER** key.

---
### 14. SSL
The next step will allow us to install (or not) a Self-Signed Certificate and therefore allow us to use HTTPS in the connection to the BC Instance.
> ![](/assets/images/local10/image21.png)

a.  The Default option, usually chosen when only using the container locally from the host computer.
b.  This option will install a self-signed SSL Certificate on the Docker Image to validate the use of HTTPS when connecting to the container through a web browser.
c.  This option is an extension to option **b** with the addition of installing the same certificate on the HOST, to remove the insecure connection warnings shown when connecting to container through a web browser.

We will pick the default option "**a**" followed by submitting it with the **ENTER** key.

---
### 15. Isolation
At this point of the wizard we are asked how the container is run.
> ![](/assets/images/local10/image22.png)

We will keep this section short and note that unless you wish to force an option, we are going to pick option "**a**" to allow the ContainerHelper to decide which isolation mode to use, followed by submitting it with the **ENTER** key.

---
### 16. MemoryLimit
This option will let us pick how much RAM Memory our BC Container is allowed to use.
> ![](/assets/images/local10/image23.png)

As the information provided in the wizard states:
-   4GB is generally used for a Demo/Test environment of Business Central
-   4G-8GB is recommended for app development.
-   16GB is recommended for base app development.

The BC Container won't be running constantly at the given RAM use, but will have the alternative to flex its use up to the limit provided.

Pick the option you require for your use, we will go with "**4G**" for this guide followed by submitting it with the **ENTER** key.

---
### 17. Save Image
This step will allow us to pick a specific name of the image we will be creating.
> ![](/assets/images/local10/image24.png)

This step has its information well provided in the Wizard for its use and while its useful, we won't be using this option and will continue by simply leaving the option **blank** followed by submitting it with the **ENTER** key.

---
### 18. PowerShell Script
Summary of the settings chosen in the wizard; picture bellow will reflect the options we have provided in this guide. Here you will also be given the option to save this script for future use and modification.
> ![](/assets/images/local10/image25.png)

To save this script, simply supply a name for the script, followed by submitting it with the **ENTER** key.

---
### 19. DONE
Once you have hit **ENTER** in the Wizard, it will follow up with opening the newly created script in PowerShell ISE, where you can run and modify it at any given time.
Once you are ready to finish this BC Container Installation, simply run the script and let it run its course.
When everything is done, you will be able to locate your new installation of the BC Docker Container within the program "**Docker Desktop**".  You will also find there are newly created shortcuts on the Desktop named for your image:
- *containername* Command Prompt - This will open a command prompt _within_ the container
- *containername* Powershell - This will open a Powershell prompt _within_ the container
- *containername* Web Client - This will open a browser using the url of the container

---

**This guide has been provided to you by "Spare Brained Ideas AB".**

If you are interested in more guides like this one, then follow us on one of the following platforms:
