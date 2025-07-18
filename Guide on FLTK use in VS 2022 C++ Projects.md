Prerequisites:
- ***FLTK***: previously installed Debug/Release (preferably both) version of library. If you haven't done it yet, check out the installation guide in this repository.
- ***VS 2022 with C++ workload***: although I assume you already have the correct setup if you're interested in this guide, I still want to make sure you did install all necessary component for proper C++ work in your IDE.

---

There are only 2 ways of configuring your project for the FLTK use that I'm aware of:
1. **Configure a single project in Options menu**
2. ***Make Property Sheets for future use in other projects***

The second way contains all steps of the first one + additional ones so I will concentrate rather on one. I'll tell you what to change if you only want one project to be configured.

## Step 1: Create Property Sheet
To create a new Property Sheet you need to open your project in VS 2022:

**Open C++ project → Solution Explorer → Right Mouse Click on the project → "Add" → "New Item..." → "Property Sheets" → "Add"

1. **Open C++ project**

![[Pasted image 20250718122238.png]]

2. **Solution Explorer**
![[Pasted image 20250718122331.png]]

3. **Right Mouse Click on the project** → **"Add"** → **"New Item..."**
![[Pasted image 20250718122659.png]]

4. **"Property Sheets"** → **"Add"**
![[Pasted image 20250718122840.png]]

If you completed these steps, you should have the Property Sheet in your project directory
![[Pasted image 20250718123038.png]]

The common structure that does not yet have the necessary settings is
![[Pasted image 20250718123344.png]]

---

## Step 2: Add Property Sheet
If you never dealt with Property Sheet, you might think: "But I just added this sheet to my project, why would I do it again".  The problem is your Property Sheet is not visible to your project and the setting won't be applied.
To active your .props file you need the Property Manager menu, which is commonly not found easily but you have me and this guide, so shouldn't be much trouble for you to do this:

**Go to "View" → "Other Windows" → "Property Manager"** 
![[Pasted image 20250718123928.png]]

After you opened Property Manager choose the **"Add Existing Property Sheet"** option
![[Pasted image 20250718124201.png]]

Usually it opens File Explorer with your project, so choose the Property Sheet you have created previously
![[Pasted image 20250718124405.png]]

Now your Property Sheet should be seen from the Property Manager in the folder that corresponds to your currently chosen building options
![[Pasted image 20250718124533.png]]

---

## Step 3: Configure Property Sheet 
To properly configure .props file you should firstly decide whether you need the Debug version or the Release one.

>[!warning] Incompatible versions
>Debug versions of app builds require Debug versions of libraries they are using. Same goes for Release versions. 

Again, I recommend having both Debug and Release versions, so you can use library in both Debug and Release builds of your applications.

To access the configuration menu right click on the .props file in Property Manager and choose **"Properties"** option

![[Pasted image 20250718125404.png]]

__This part is for single project configuration__
You have to access the same **"Properties"** menu but from another place. 
In your Solution Explorer window right click on the Project and choose **"Properties"** in the bottom of the menu. Next steps will be the same as for the Property Sheet configuration
![[Pasted image 20250718125738.png]]

Firstly you need to include library in your project, so follow

**"Common Properties" → "C/C++" → "General" → "Additional Include Directories"

![[Pasted image 20250718130324.png]]

Click on the arrow and **"Edit**
![[Pasted image 20250718130402.png]]

In opened window choose the folder icon 
![[Pasted image 20250718130553.png]]

and then click on **"..."**, this will open File Explorer where you must navigate to directory where you installed FLTK library, here we have two options - Debug/Release

**Debug**:
Choose the directory with Debug version of the library if you configure Property Sheet for Debug builds, for me its `fltk_debug` folder, choose the `include` folder and confirm selection
![[Pasted image 20250718130926.png]]

**Release**:
Choose the directory with Release version of the library if you configure Property Sheet for Release builds, for me its `fltk_release` folder, choose the `include` folder and confirm selection
![[Pasted image 20250718131247.png]]

Just for this demo I chose the Debug version.
Confirm selection once again
![[Pasted image 20250718131359.png]]

The next step is to configure C++ Linker. Go to **"Linker" → "General"**
![[Pasted image 20250718131936.png]]

Now click on arrow and follow the same steps as before but this time you need the `lib` folder. Again, you have 2 choices - Debug/Release, choose the version you have chosen for previous selection and stick with it:

**Debug**:
![[Pasted image 20250718132220.png]]

**Release**: Just choose the Release version of library.

After this, go to **"Linker" → "Input" → "Additional Dependencies"

![[Pasted image 20250718132508.png]]

Edit it by adding a list of specified dependencies, there are 2 versions of them also - Debug/Release, I'll leave both in separate text files, be sure to choose the correct one
![[Pasted image 20250718132755.png]]

Apply all changes and return to Property Manager to complete configuration. Click on the save icon to save you .props file
![[Pasted image 20250718133001.png]]

It should look something like this 
![[Pasted image 20250718133041.png]]

If it does, congrats! You have successfully configured reusable settings for your project! 

---

## Conclusion
I hope you haven't ran into a problem along this little journey. Now you can use the FLTK Property Sheet in any project but be sure to activate it first through Property Manager. And remember - never mix Debug with Release (yes, it was very painful for me to fuck up and have 263 compiler errors related to Linker).