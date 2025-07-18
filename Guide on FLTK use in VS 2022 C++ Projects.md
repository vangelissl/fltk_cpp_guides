Prerequisites:
- ***FLTK***: previously installed Debug/Release (preferably both) version of library. If you haven't done it yet, check out the installation guide in this repository.
- ***VS 2022 with C++ workload***: although I assume you already have the correct setup if you're interested in this guide, I still want to make sure you did install all necessary component for proper C++ work in your IDE.

>**Common pitfalls**:
>This is again related to the Debug/Release versions mismatch.
>Possible scenarios:
>- You mix Debug directories/libs with Release directories in Properties configuration - the result is likely invalid project config/.props file.
>- You are trying to use Debug build of application with Release build of the FLTK library or otherwise - the result is commonly a bunch of errors related to `_ITERATOR_DEBUG_LEVEL` and classified as Linker errors.

---

There are only 2 ways of configuring your project for the FLTK use that I'm aware of:
1. **Configure a single project in Properties menu**
2. **Make Property Sheets for future use in other projects**

The second way contains all steps of the first one + additional ones so I will concentrate rather on one. I'll tell you what to change if you only want one project to be configured.

## Step 1: Create Property Sheet
To create a new Property Sheet you need to open your project in VS 2022:

**Open C++ project → Solution Explorer → Right Mouse Click on the project → "Add" → "New Item..." → "Property Sheets" → "Add"**

1. **Open C++ project**
   
<img width="1916" height="1020" alt="Pasted image 20250718122238 1 1" src="https://github.com/user-attachments/assets/e13bdbaa-20ea-4c54-8b99-8ab7f121ddf6" />


3. **Solution Explorer**
   
<img width="510" height="303" alt="Pasted image 20250718122331" src="https://github.com/user-attachments/assets/f71b7566-e292-414f-a566-61f5ae892a53" />


5. **Right Mouse Click on the project** → **"Add"** → **"New Item..."**
   
<img width="905" height="1018" alt="Pasted image 20250718122544" src="https://github.com/user-attachments/assets/aa6f21f9-dfb1-4d91-ab73-b971d086af35" />


7. **"Property Sheets"** → **"Add"**
   
<img width="1177" height="816" alt="Pasted image 20250718122840" src="https://github.com/user-attachments/assets/0275d7a7-29be-4e68-afd3-e896f582dca2" />


If you completed these steps, you should have the Property Sheet in your project directory

<img width="485" height="340" alt="Pasted image 20250718123038" src="https://github.com/user-attachments/assets/4a8b13bc-de9d-4b58-b6d1-7a3fa74e3b1a" />


The common structure that does not yet have the necessary settings is

<img width="856" height="230" alt="Pasted image 20250718123344" src="https://github.com/user-attachments/assets/3ea3e0c4-58c6-4aed-820d-84ee9e5a11fd" />


---

## Step 2: Add Property Sheet
If you never dealt with Property Sheet before, you might think: "But I just added this sheet to my project, why would I do it again".  The problem is your Property Sheet is not visible to your project and the setting won't be applied.
To active your .props file you need the Property Manager menu, which is commonly not found easily but you have me and this guide, so shouldn't be much trouble for you to do this:

**Go to "View" → "Other Windows" → "Property Manager"** 
<img width="1013" height="1000" alt="Pasted image 20250718123928" src="https://github.com/user-attachments/assets/31628706-34e6-450b-b70e-933550a9b51e" />

After you opened Property Manager choose the **"Add Existing Property Sheet"** option
<img width="740" height="335" alt="Pasted image 20250718124201" src="https://github.com/user-attachments/assets/5dddffe8-66ad-49e8-9ad8-c8e22b4f7234" />

Usually it opens File Explorer with your project, so choose the Property Sheet you have created previously
<img width="962" height="603" alt="Pasted image 20250718124405" src="https://github.com/user-attachments/assets/531ae1d8-cbb3-448b-9006-066ec4946ff7" />


Now your Property Sheet should be seen from the Property Manager in the folder that corresponds to your currently chosen building options
<img width="684" height="345" alt="Pasted image 20250718124533" src="https://github.com/user-attachments/assets/00229440-239b-4ed9-9657-8fb71acddbe9" />


---

## Step 3: Configure Property Sheet 
To properly configure .props file you should firstly decide whether you need the Debug version or the Release one.

>[!warning] Incompatible versions
>Debug versions of app builds require Debug versions of libraries they are using. Same goes for Release versions. 

Again, I recommend having both Debug and Release versions, so you can use library in both Debug and Release builds of your applications.

To access the configuration menu right click on the .props file in Property Manager and choose **"Properties"** option

<img width="625" height="420" alt="Pasted image 20250718125404" src="https://github.com/user-attachments/assets/29841c91-e5ce-43af-97be-fe451d2a8c66" />


__This part is for single project configuration__
You have to access the same **"Properties"** menu but from another place. 
In your Solution Explorer window right click on the Project and choose **"Properties"** in the bottom of the menu. Next steps will be the same as for the Property Sheet configuration

<img width="620" height="978" alt="Pasted image 20250718125738" src="https://github.com/user-attachments/assets/3f8726d9-7aff-4a60-86ab-3aee9bfaf0a0" />


Firstly you need to include library in your project, so follow

**"Common Properties" → "C/C++" → "General" → "Additional Include Directories"**

<img width="1001" height="685" alt="Pasted image 20250718130324" src="https://github.com/user-attachments/assets/1d805ebb-6728-4786-8522-5576b89c0b6e" />


Click on the arrow and **"Edit**

<img width="708" height="114" alt="Pasted image 20250718130402" src="https://github.com/user-attachments/assets/01c58e41-30f2-40e3-bd79-29209f06acd8" />


In opened window choose the folder icon

<img width="473" height="479" alt="Pasted image 20250718130553" src="https://github.com/user-attachments/assets/68c91ffa-011a-49cb-854b-60d17ec58c05" />


and then click on **"..."**, this will open File Explorer where you must navigate to directory where you installed FLTK library, here we have two options - Debug/Release

**Debug**:
Choose the directory with Debug version of the library if you configure Property Sheet for Debug builds, for me its `fltk_debug` folder, choose the `include` folder and confirm selection

<img width="938" height="589" alt="Pasted image 20250718130926" src="https://github.com/user-attachments/assets/32c1632d-45a4-4e56-9701-4af8ba10160c" />


**Release**:
Choose the directory with Release version of the library if you configure Property Sheet for Release builds, for me its `fltk_release` folder, choose the `include` folder and confirm selection

<img width="952" height="597" alt="Pasted image 20250718131247" src="https://github.com/user-attachments/assets/95ea32ce-e51e-4486-84bf-0ff25880c172" />


Just for this demo I chose the Debug version.
Confirm selection once again

<img width="476" height="490" alt="Pasted image 20250718131359" src="https://github.com/user-attachments/assets/f3fe860e-2219-41d2-8ed5-e58b0637e2e7" />


The next step is to configure C++ Linker. Go to **"Linker" → "General"**

<img width="995" height="678" alt="Pasted image 20250718131936" src="https://github.com/user-attachments/assets/f3a07579-c25e-40dd-bc12-915e83522dba" />


Now click on arrow and follow the same steps as before but this time you need the `lib` folder. Again, you have 2 choices - Debug/Release, choose the version you have chosen for previous selection and stick with it:

**Debug**:

<img width="953" height="597" alt="Pasted image 20250718132220" src="https://github.com/user-attachments/assets/9aa0e1a9-429b-4b06-9ca9-18f6adf6bf22" />


**Release**: Just choose the Release version of library.

After this, go to **"Linker" → "Input" → "Additional Dependencies"

<img width="997" height="683" alt="Pasted image 20250718132508" src="https://github.com/user-attachments/assets/037ea16a-7c6f-4a18-9b90-b34ba9944e78" />


Edit it by adding a list of specified dependencies, there are 2 versions of them also - Debug/Release, I'll leave both in separate text files, be sure to choose the correct one

<img width="472" height="475" alt="Pasted image 20250718132755" src="https://github.com/user-attachments/assets/36d25e45-c29a-4c18-acb1-a753713f91cc" />


Apply all changes and return to Property Manager to complete configuration. Click on the save icon to save you .props file

<img width="607" height="331" alt="Pasted image 20250718133001" src="https://github.com/user-attachments/assets/ea19ae61-be86-434b-974a-5ef0e7d62255" />


It should look something like this 

<img width="1674" height="398" alt="Pasted image 20250718133041" src="https://github.com/user-attachments/assets/64d10220-e1b8-4e92-8c96-1a3b718d65eb" />


If it does, congrats! You have successfully configured reusable settings for your project! 

---

## Conclusion
I hope you haven't ran into a problem along this little journey. Now you can use the FLTK Property Sheet in any project but be sure to activate it first through Property Manager. And remember - never mix Debug with Release (yes, it was very painful for me to fuck up and have 263 compiler errors related to Linker).
