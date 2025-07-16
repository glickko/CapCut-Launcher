

---
### **DISCLAIMER**
---
I create this launcher after CapCut last release in last year.
and I need to be very clear about this: I made this tool for educational and research purposes only. The goal is to show the CapCut developers where some of the holes are in their software, especially with `VECreator.dll` `VESafeGuard.dll`.

- This Launcher is not Public shareable, and i think this is best strings i found ever, i already trying many strings still get internet error in many version. and yeah if you want it, you can try this via DM my discord all in your own risk.


Bypassing:
Pro Export Features,
Login,
Internet Error Limited Export


**WARNING**
I don't support piracy or any illegal stuff. Please don't use this to make money or get around buying the software. If you use this tool, you're agreeing that it's for your own education and you're using it at your own risk. I'm not responsible for what you do with it.

**Heads up: This is only meant to work with CapCut version i Patched**

---
### **HOW TO USE**
---
<h1>Check out how to use this thing:</h1>

<video width="720" controls>
  <source src="./assets/How To Use.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
Getting this to work is super easy.

**1. Installation:**
   - Just drop my `CC-Launcher.exe` into the same folder as your CapCut installation. It should look like this:
     ```
     Original-Capcut-Folder/
     |-- CapCut xxx Version     <-- CapCut main dir.installation
     |   |-- CapCut.exe
     |   |-- ...
     |
     |-- CC-Launcher.exe  <-- My launcher
     ```

**2. Running the Launcher:**
   - Right-click `CC-Launcher.exe` and hit "Run as administrator". It needs admin rights to do its thing in the CapCut folder.

**3. The Buttons:**
   - **PATCHED (Offline Export):** Click this to apply my patch. It lets you edit and export without logging in or needing Pro, but it will turn off the online Pro features. CapCut will start up right after.
   - **UNPATCHED (Online Features):** Click this to go back to normal. It restores everything so you can log in and use all the online stuff again. CapCut will start up right after.
   - **Force Close CapCut:** If CapCut freezes up, this button will take care of it.

**4. Exiting:**
   - When you close my launcher, it automatically force-closes CapCut and puts everything back to the original, unpatched state. This makes sure your system is left totally clean.

---
### **HOW MY LAUNCHER WORKS**
---

This patch is the result of a standard reverse engineering workflow. The launcher simply automates the final steps. Here's the real process I followed to find the vulnerabilities.

**1. Static Analysis (Ghidra):**
   - The first step was to load `VECreator.dll` into Ghidra to decompile the assembly code. I started by searching for interesting strings like "isPro", "isVip", "getLoginStatus", and "watermark" this is just exsample, truly i found another string not from that strings. This gave me a list of potential functions that control the application's premium features, login, and cloud checking.

**2. The Anti-Debug Challenge (VESafeGuard.dll):**
   - I quickly discovered that trying to attach a debugger like x64dbg would cause the application to crash immediately. This is because of `VESafeGuard.dll`, a security module designed specifically to prevent debugging.

**3. Bypassing the Anti-Debug:**
   - To get around this, I had to create my own custom hook DLL. The purpose of this DLL was to intercept the calls to the anti-debug functions within `VESafeGuard.dll` before they could execute. By hooking these functions and making them return "success" (or doing nothing at all), I effectively disabled the anti-debug protection. This method named `IAT Hooking` im also making cheat, and IAT is work perfectly in this Software, another Hooking method you can learn from underground forum if you want. This just for education, how S.Enginering is working.

**4. Dynamic Analysis (x64dbg + Plugins):**
   - With the anti-debug bypassed, I could now attach x64dbg to the running CapCut process. I used plugins like ScyllaHide to further mask the debugger's presence.
   - I set breakpoints on the functions I had identified in Ghidra. By triggering Pro features and Log In, in the app, I could hit these breakpoints and step through the code line-by-line. This allowed me to see exactly which conditional jumps (`JNE`, `JNZ`, `ret`, `null`, etc.) were responsible for the "access denied" logic.

**5. Automation (This Launcher):**
   - The final step was to make these changes permanent without needing a debugger every time. I noted the exact hex bytes of the conditional jumps I wanted to bypass.
   - This launcher automates that final step. When you click "PATCHED," it reads the user's `VECreator.dll` into memory, applies the necessary hex changes to neutralize the security checks, and saves the modified file. The loader files are deployed to handle any other necessary hooks. This provides a simple, one-click solution that uses the information discovered during the reverse engineering process.

