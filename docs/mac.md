# Mac (UTM on ARM) instructions for laptop-homelab-starterkit

Note: These instructions assume that you use an Apple Silicon Mac.

Please also note that this is for testing purposes and not properly secured (by design). Do not put any confidential or sensitive data into the system that we set up here.

## Part 1. Setting up the host

1. Install UTM
	- Option 1. Go to https://mac.getutm.app/ and click **Download**. Open the downloaded DMG file and then drag the app to `/Applications/`
	- Option 2. Set up Homebrew (https://brew.sh/) and then run `brew install --cask utm`
		- There are ongoing debates about the security implications of Homebrew. [For example](https://security.stackexchange.com/questions/191364/what-are-the-security-implications-of-homebrew-and-macports) how Homebrew alters permissions on certain folders in order facilitate automated installations. Please take into consideration whether or not this is a risk in your case depending on who has access to your machine.
	- Option 3. Go to https://mac.getutm.app/ and click **Mac App Store**.
		- Note that this will cost money! You do _not_ need to use this option unless you want to.
		- As per the UTM website: _"The Mac App Store version is identical to the free version and there are no features left out of the free version. The only advantage of the Mac App Store version is that you can get automatic updates. Purchasing the App Store version directly funds the development of UTM and shows your support ."_

2. Download Debian
	- Go to https://cdimage.debian.org/debian-cd/current/arm64/iso-dvd/ and download the file whose filename ends with `-arm64-DVD-1.iso`. It should be about 3.7G in size.
	- You will receive a file named something like `debian-12.9.0-arm64-DVD-1.iso`, the important thing is that the file has the `arm64` in the filename.

3. Open UTM and click **Create a New Virtual Machine**. Then, when prompted, click **Virtualize**, then click **Linux**.

4. When asked about Virtualization Engine and Boot Image Type, do not change the default settings. However, when asked about **Boot ISO Image**, navigate to and select the `iso` file from Step 2, then click **Continue**.

5. When asked about Hardware, assign 512 MiB of Memory, and 1 CPU core only. Do not "enable hardware OpenGL acceleration" as you do not need that. Then click **Continue**.

6. When asked about Storage, assign only 2 GiB of Storage. Then click **Continue**.

7. When asked about Shared Directory, do not set up any shared directories. Then click **Continue**.

8. On the summary page, give the virtual machine the name **debian001**. Then click **Save**.

<!-- 9. Right-click on the debian001 entry in the left-hand-side menubar. Then click **Edit**.

10. Click on **QEMU** and then switch OFF the option named **UEFI Boot**. -->

&nbsp;

_Discussion questions:_

- Q1. Which option did you decide to take for Step 1 (Install UTM), and how did you make that decision?

- Q2. Step 1 refers to security implications of Homebrew. Explain the technical details of the concern about how Homebrew alters permissions on certain folders.

- Q3. Step 2 delivered an `iso` file to your laptop. Which server did it come from and how can we find out more about that server?

- Q4. It is important to verify the checksum of the `iso` file that we received. How can we do that? (Note: you may need to do some independent research about this.)

- Q5. What supply chain risks exist here, and what could we do to mitigate them?

## Part 2. Setting up the guest

1. Start the virtual machine **debian001**. A new window will appear and soon it will look something like this:

![debian001-boot-screen](../images/debian001-boot-screen.png)

2. This is a command-line interface, not a graphical user interface. Use the arrow keys on your keyboard to navigate up and down the different options to try it out, but we actually want to use the default option called ***Install** (the first on the list). Select it and then hit <kbd>ENTER</kbd> on your keyboard.

3. Once you are in the Debian installer, please read the text in the bottom-left corner: _"&lt;Tab&gt; moves; &lt;Space&gt; selects; &lt;Enter&gt; activates buttons"_. Make sure that you do likewise for the remainder of the Debian installer.

4. For the language, select **English**. For the location, select **Ireland** (unless you are elsewhere?).

5. For the keyboard keymap, do a quick bit of research to find out what kind of keyboard you have. For example, my MacBook was purchased in Australia, which uses the **American English** keymap. This page may be helpful: https://support.apple.com/en-ie/102743

6. After the above steps, the installer will perform some tasks automatically, and then you will be asked to specify the hostname. Please use the hostname **debian001**. When asked about the domain name, though, just keep that blank.

7. When asked about the root password, just enter it as `password`. Yes, really! This is just a testing system as per the note at the top of this page.

8. When asked for the full name of the new user, enter your name in lowercase. For example I entered `blair`. Then confirm that this is the username of your account, and set your account to also have the password just as `password`.

9. When asked about partitioning disks, select the default **Guided - use entire disk**, and then allow it to use the default **Virtual disk 1 (vda) - 2.1 GB Virtio Block Device**. Then when prompted, accept the default setting **All files in one partition (recommended for new users)**.

10. When invited to, please confirm the partitioning plan:

![debian001-confirm-partitioning-plan](../images/debian001-confirm-partitioning-plan.png)

11. When prompted to "write the changes to disk", select **&lt;Yes&gt;**.

12. When prompted to "scan extra installation media", select **&lt;No&gt;**.

13. When prompted to configure a Debian archive mirror country, select **&lt;No&gt;**.

14. Do not participate in the package usage survey.

15. When prompted to "choose software to install", keep the default selection of **SSH server** and **standard system utilities**.

![debian001-software-selection](../images/debian001-software-selection.png)




&nbsp;

_Discussion questions:_

- Q6. The screenshot below Step 1 refers to "GNU GRUB". What is this? (Note: you may need to do some independent research about this.)

- Q7. The screenshot below Step 10 refers to `ext4` and `swap`. What are these, and what are the security implications of them?

- Q13. Step 13 refers to "mirrors". What are these?

- Q15. The screenshot below step 15 refers to various desktop environments. What are these?

