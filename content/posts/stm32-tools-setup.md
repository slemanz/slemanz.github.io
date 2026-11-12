+++
authors = ["William Sleman"]
title = "Setting Up the Tools for STM32 Bare-Metal Development"
date = "2026-11-12"
draft = true
description = "Step-by-step install of every tool used in the STM32 Embedded Fundamentals course, on Windows and Linux."
tags = [
    "firmware",
]
categories = [
    "embedded systems",
]
+++

This is the install guide for my course **STM32 Embedded Fundamentals**. It covers every
tool we use, on Windows and on Linux, and how to check that each one works.

<!--more-->

I keep this page up to date. If a download page changed and something here doesn't
match, tell me (contact link at the top) and I'll fix it.

<!-- DRAFT: every line marked [VERIFY] must be checked on a clean machine before publishing. -->

## What you'll install

| # | Tool | What it's for |
|---|------|---------------|
| 1 | Git (Git Bash on Windows) | One terminal with the same commands on Windows and Linux |
| 2 | GCC | Compiles C for your PC |
| 3 | Make | Runs the build |
| 4 | Arm GNU Toolchain 12.3.Rel1 | Compiles C for the chip (`arm-none-eabi-gcc`) |
| 5 | Python | Helper scripts used later in the course |
| 6 | VS Code | The editor (any editor works) |
| 7 | PuTTY | Serial terminal |
| 8 | STM32CubeProgrammer | ST-Link USB driver and probe firmware updates (Windows only) |
| 9 | J-Link Software | Only if you have a J-Link |
| 10 | OpenOCD | Flashes the chip, with the ST-Link or the J-Link |

**Use the same versions as the course**, especially the Arm toolchain. Same version, same
output, same warnings, same code size.

## Two ideas before you start

**The PATH.** It's a list of folders. When you type a command, the terminal looks for the
program in each of these folders. If it isn't in any of them, you get
`command not found`. For most tools below, you add the tool's `bin` folder to the PATH.

**Reopen the terminal.** A terminal that was already open doesn't see a new PATH. After
every PATH change, close the terminal and open a new one.

---

## Windows

The pattern for every tool: download → extract or install → add the `bin` folder to the
PATH → close and reopen Git Bash → check with `--version`.

Small tools go in `C:\tools`. **No spaces in the path**: some build tools break on
`C:\Program Files\...`.

### How to edit the PATH on Windows

You'll do this several times, always the same way:

1. Start menu → type `environment` → open **Edit the system environment variables**.
2. Click **Environment Variables…**.
3. Under **User variables**, select **Path** → **Edit**.
4. **New** → paste the folder → **OK** → **OK** → **OK**.
5. Close Git Bash and open it again.

<!-- IMAGE: win-path-edit.png — the "Edit environment variable" window with the list of
folders and the New button highlighted. -->

### 1. Git for Windows (Git Bash)

1. Go to [git-scm.com](https://git-scm.com/) → **Download for Windows** → 64-bit installer.
2. Run it. The defaults are fine, except:
   - **Select Components**: check **Add a Git Bash Profile to Windows Terminal**.
     [VERIFY: name and default state of this checkbox]
   - **Choosing the default editor used by Git**: pick **Notepad** (the default is Vim,
     which is hard to exit if you never used it).

<!-- IMAGE: win-git-components.png — Select Components, with the Windows Terminal profile
checkbox highlighted. -->

**Open Git Bash inside Windows Terminal.** Windows Terminal has a better font, tabs and
easy copy/paste. It comes with Windows 11; on Windows 10, install it from the Microsoft
Store.

1. Open **Terminal** → **Settings** (`Ctrl+,`) → **Startup**.
2. **Default profile**: **Git Bash** → **Save**.
3. Close and reopen Terminal: it now starts in Git Bash. Pin it to the taskbar.

From now on, "Git Bash" means this window.

```bash
git --version
```

### 2. GCC (MinGW-w64 8.1.0)

1. Download
   [x86_64-8.1.0-release-posix-seh-rt_v6-rev0.7z](https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/8.1.0/threads-posix/seh/x86_64-8.1.0-release-posix-seh-rt_v6-rev0.7z/download).
2. Extract it to `C:\`. You get `C:\mingw64\bin\gcc.exe`.
   Recent Windows 11 opens `.7z` files directly; otherwise install [7-Zip](https://www.7-zip.org/).
3. Add `C:\mingw64\bin` to the PATH, then reopen Git Bash.

{{< notice warning >}}
Don't use the big green "Download Latest Version" button on the MinGW-w64 project page:
that's the source code, not the compiler.
{{< /notice >}}

```bash
gcc --version     # gcc.exe (x86_64-posix-seh-rev0, Built by MinGW-W64 project) 8.1.0
```

### 3. Make (GnuWin32 3.81)

1. Go to [gnuwin32.sourceforge.net/packages/make.htm](https://gnuwin32.sourceforge.net/packages/make.htm).
2. In the row **Complete package, except sources**, click **Setup** and run the installer
   with the defaults.
3. Add `C:\Program Files (x86)\GnuWin32\bin` to the PATH, then reopen Git Bash.

Use the Setup program, not the zip with only the binaries: that one is missing DLLs and
`make` won't start. The space in `Program Files` is fine here, because it's only in the
PATH; our Makefiles never point to it.

```bash
make --version    # GNU Make 3.81
```

### 4. Arm GNU Toolchain 12.3.Rel1

1. Download
   [arm-gnu-toolchain-12.3.rel1-mingw-w64-i686-arm-none-eabi.zip](https://developer.arm.com/-/media/Files/downloads/gnu/12.3.rel1/binrel/arm-gnu-toolchain-12.3.rel1-mingw-w64-i686-arm-none-eabi.zip)
   (the zip, not the `.exe` installer).
   It's also on the [Arm downloads page](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads),
   under 12.3.Rel1 → Windows → AArch32 bare-metal target (arm-none-eabi).
2. Create `C:\tools` and extract the zip there, so you get:
   `C:\tools\arm-gnu-toolchain-12.3.rel1-mingw-w64-i686-arm-none-eabi\bin\arm-none-eabi-gcc.exe`
   [VERIFY: whether the zip creates a top-level folder or a double folder]
3. Add that `bin` folder to the PATH, then reopen Git Bash.

```bash
arm-none-eabi-gcc --version   # arm-none-eabi-gcc (Arm GNU Toolchain 12.3.Rel1 (Build arm-12.35)) 12.3.1 20230626
```

### 5. Python

1. Go to [python.org](https://www.python.org/downloads/) → download the latest Python 3.
2. On the first screen of the installer, check **Add python.exe to PATH** → **Install Now**.

<!-- IMAGE: win-python-path.png — first installer screen with "Add python.exe to PATH"
checked. -->

```bash
python --version
```

{{< notice tip >}}
If typing `python` opens the Microsoft Store, Python isn't in the PATH. Search for
**Manage app execution aliases**, turn off the two Python entries, and run the installer
again with the box checked.
{{< /notice >}}

### 6. VS Code

1. Go to [code.visualstudio.com](https://code.visualstudio.com/) → **Download for Windows**
   (User Installer).
2. On **Select Additional Tasks**, keep **Add to PATH** checked.
3. Reopen Git Bash and install the extensions:

```bash
code --version
code --install-extension ms-vscode.cpptools
code --install-extension ms-python.python
code --list-extensions
```

I also use the Vim extension (`vscodevim.vim`). If you don't know Vim, don't install it:
it changes how every key works, and it's not part of the course.

### 7. PuTTY

1. Go to [putty.org](https://www.putty.org/) → download page → **MSI (Windows Installer)**,
   64-bit x86 → install with the defaults.
2. Open it from the Start menu and check that **Connection type** has a **Serial** option.

No PATH this time.

### 8. STM32CubeProgrammer (ST-Link driver)

We don't flash with it in the course (OpenOCD does that), but it installs the ST-Link USB
driver and can update the firmware of the probe, which some clones need.

1. Go to [st.com/en/development-tools/stm32cubeprog.html](https://www.st.com/en/development-tools/stm32cubeprog.html)
   → **Get Software** → **STM32CubePrg-Win64**. ST asks for a free account or an e-mail.
2. Unzip and run `SetupSTM32CubeProgrammer_win64.exe` with the defaults. Accept the
   ST-Link driver install when it asks.
3. Add `C:\Program Files\STMicroelectronics\STM32Cube\STM32CubeProgrammer\bin` to the
   PATH, then reopen Git Bash. [VERIFY: install folder]

```bash
STM32_Programmer_CLI --version
```

[VERIFY: `--version` vs `-version`]

### 9. J-Link Software (only if you have a J-Link)

1. Go to [segger.com/downloads/jlink](https://www.segger.com/downloads/jlink/) →
   **J-Link Software and Documentation Pack** → Windows 64-bit installer → defaults.
2. Add `C:\Program Files\SEGGER\JLink_V<version>` to the PATH, then reopen Git Bash.
   [VERIFY: folder name]

```bash
JLink.exe
```

It prints its version and can't find a J-Link (nothing is connected). Type `exit`.
[VERIFY: whether it needs `winpty JLink.exe` inside Git Bash]

### 10. OpenOCD (xPack 0.12.0-7)

1. Go to [github.com/xpack-dev-tools/openocd-xpack/releases](https://github.com/xpack-dev-tools/openocd-xpack/releases/tag/v0.12.0-7)
   → **Assets** → `xpack-openocd-0.12.0-7-win32-x64.zip`.
2. Extract it to `C:\tools`, so you get `C:\tools\xpack-openocd-0.12.0-7\bin\openocd.exe`.
3. Add `C:\tools\xpack-openocd-0.12.0-7\bin` to the PATH, then reopen Git Bash.

```bash
openocd --version   # xPack Open On-Chip Debugger 0.12.0+dev...
```

[VERIFY: exact first line of the output]

---

## Linux (Ubuntu)

Most tools come from `apt`. The Arm toolchain is installed by hand, so you get exactly
12.3.Rel1. Open a terminal (`Ctrl+Alt+T`) and go one tool at a time.

### 1. Git

```bash
sudo apt update
sudo apt install git
git --version
```

### 2. GCC and Make

Both come in `build-essential`:

```bash
sudo apt install build-essential
gcc --version
make --version
```

### 3. Arm GNU Toolchain 12.3.Rel1

Download
[arm-gnu-toolchain-12.3.rel1-x86_64-arm-none-eabi.tar.xz](https://developer.arm.com/-/media/Files/downloads/gnu/12.3.rel1/binrel/arm-gnu-toolchain-12.3.rel1-x86_64-arm-none-eabi.tar.xz),
then extract it into `~/opt/tools`:

```bash
mkdir -p ~/opt/tools
cd ~/Downloads
tar xf arm-gnu-toolchain-12.3.rel1-x86_64-arm-none-eabi.tar.xz -C ~/opt/tools
ls ~/opt/tools/arm-gnu-toolchain-12.3.rel1-x86_64-arm-none-eabi/bin
```

Add its `bin` folder to the PATH. On Linux, the PATH is set in `~/.bashrc`, which bash
reads every time a terminal opens:

```bash
nano ~/.bashrc
```

Add this line at the end, save (`Ctrl+O`, `Enter`) and exit (`Ctrl+X`):

```bash
export PATH="$HOME/opt/tools/arm-gnu-toolchain-12.3.rel1-x86_64-arm-none-eabi/bin:$PATH"
```

Close the terminal, open a new one, and check:

```bash
arm-none-eabi-gcc --version
```

### 4. Python

Python 3 is already installed on Ubuntu. Add pip:

```bash
sudo apt install python3-pip
python3 --version
```

On Linux the command is `python3`, not `python`.

### 5. VS Code

Download the `.deb` from [code.visualstudio.com](https://code.visualstudio.com/), then:

```bash
cd ~/Downloads
sudo apt install ./code_*.deb
code --version
code --install-extension ms-vscode.cpptools
code --install-extension ms-python.python
```

### 6. PuTTY

```bash
sudo apt install putty
sudo usermod -aG dialout $USER
```

The serial port belongs to the `dialout` group. The second command adds your user to it;
it only takes effect after you **log out and log back in**.

### 7. ST-Link

Nothing to install: OpenOCD talks to the ST-Link directly.

### 8. J-Link Software (only if you have a J-Link)

Download the **Linux 64-bit DEB installer** from
[segger.com/downloads/jlink](https://www.segger.com/downloads/jlink/), then:

```bash
cd ~/Downloads
sudo apt install ./JLink_Linux_*_x86_64.deb
JLinkExe
```

Type `exit` to leave. The package also installs the udev rules, so the J-Link works
without `sudo`.

### 9. OpenOCD

```bash
sudo apt install openocd
openocd --version
```

The package installs the udev rules for the probes, so you can flash without `sudo`.
Version 0.11 or newer works for the course. [VERIFY: apt version on Ubuntu 22.04 / 24.04]

---

## Final check

Open a **new** terminal and run everything:

**Windows (Git Bash)**

```bash
git --version
gcc --version
make --version
arm-none-eabi-gcc --version
python --version
code --version
STM32_Programmer_CLI --version
openocd --version
```

**Linux**

```bash
git --version
gcc --version
make --version
arm-none-eabi-gcc --version
python3 --version
code --version
openocd --version
```

Plus PuTTY (opens, has **Serial**) and, if you have one, the J-Link (`JLink.exe` /
`JLinkExe`, then `exit`).

### What you should see

| Tool | Windows | Linux |
|------|---------|-------|
| `arm-none-eabi-gcc` | 12.3.Rel1 | 12.3.Rel1 |
| `gcc` | 8.1.0 | your distro's (11.4.0 on Ubuntu 22.04) |
| `make` | 3.81 | your distro's (4.3 on Ubuntu 22.04) |
| `python` / `python3` | 3.x | 3.x |
| `openocd` | 0.12.0 (xPack) | 0.11 or newer |

### If something fails

- **`command not found`**: the tool's `bin` folder isn't in the PATH, or the terminal was
  open before you changed it. Check the folder, then close and reopen the terminal.
- **`python` opens the Microsoft Store**: see the tip in step 5.
- **Wrong version** (for example, another `arm-none-eabi-gcc` from an old install): run
  `which arm-none-eabi-gcc` to see which one the terminal finds first.

Everything shows a version? You're ready for the next lesson.
