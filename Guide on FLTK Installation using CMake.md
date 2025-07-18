Prerequisites:
- ***CMake*** installed, if not, use this go to https://cmake.org/download/.
- ***Git*** if you would prefer cloning the repository from Github.
- ***OS***: Windows as I never tested it with other OS, in case of other OS configure proper generator with appropriate C++ compiler installed.
- ***C++ compiler***: Visual Studio 2022 with C++ workload is recommended as I was using it in my case.

If you don't trust this guide or something here didn't work for you, or you are using different OS/generator/IDE, I strongly recommend checking the official [guide](https://github.com/fltk/fltk/blob/master/README.CMake.txt) in git repository which is less verbose and detailed but 100% truthworthy.

---
## Step 1: Clone or Download FLTK
I recommend cloning a GitHub repo, otherwise you have to deal with **tar.zp** extension.
Just navigate to directory where you want to store the repo and use this command: 

`git clone https://github.com/fltk/fltk.git`

If you chose to stick up with the archive version, go to https://www.fltk.org/software.php

---
## Step 2: Generate Build System
Firstly, you need to navigate to FLTK root directory which is probably **whatever_folder_you_chosen\fltk**. From the root you need to run the command in terminal: 
`cmake -B build`

I believe the default settings are used if not specified otherwise but in my case I was using `"Visual Studio 17 2022"` generator and another option of that kind that I'm aware of is `"Ninja"`. 
Other available option is the `CMAKE_BUILD_TYPE` with 2 options - `Release` and `Debug`, you can only build each of these types separately so in case you need both, you'll need to run the command two times.
You can choose either Release of Debug version if you know what you need but if not, I recommend building both as there might be a big chance you'll eventually need both.
Also, you have to make sure your default projects architecture is the same as the one you specify by `-A <arch>` parameter, I usually use `x64` so I went with it, in case of incompatibility you'll end up with errors.
The command I used to build my Release and Debug versions was:

`cmake -B build -G "Visual Studio 17 2022" -A x64 -D CMAKE_BUILD_TYPE=Release`

and 
`cmake -B build -G "Visual Studio 17 2022" -A x64 -D CMAKE_BUILD_TYPE=Release`

respectively
If you're not sure about the parameters, do some research and find the ones that are suitable for you.

---

## Step 3: Build FLTK
This is the final step to build a working version of library. The previously generated build systems would be used in building a library itself, that means you cannot build a Debug version if you only have the Release version build system. That said, I strongly recommend having both on hands.
The default command that build a Debug version of library:

`cmake --build build`

or alternatively

`cmake --build build --config Debug` 

which, I believe, is the same command rather more verbose and explicit.
For Release version you do the same thing but with `--config Release`.

---

## Step 4: Install FLTK
Commands below allow you to install the previously built working version of FLTK, both Debug and Release:

**Default**:
`cmake --install build`

**Specified parameters (version, path)**:
`cmake --install build --config <Release/Debug> --prefix <your_path>`

fill the `<*>` with your preferences.

---

## Conclusion 
Having built the working FLTK library you can use it in your VS 2022 projects. I will leave the guide on how to configure the project for the use of library in this same repository. 
Sincerely hope I could help whoever used this guide!
