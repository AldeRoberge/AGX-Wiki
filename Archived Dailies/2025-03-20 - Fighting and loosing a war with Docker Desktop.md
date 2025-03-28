---
tags:
  - docker
  - WSL
  - troubleshooting
  - admin-privileges
date: 2025-03-20
title: Fighting and loosing a war with Docker Desktop
---
## Introduction

Docker is a brilliant idea—containerizing applications to create portable, isolated environments is a game-changer. However, as with many great ideas, the devil lies in the details. My experience has been a constant fight with Docker, especially when mixed with the peculiarities of a work setup that forces a constant juggling act between a work account and an admin account. In this note, I share my journey, the obstacles encountered, and the steps that ultimately helped resolve the issues.

Despite Docker’s solid conceptual foundation, its execution has been anything but smooth in my environment. I’ve encountered a series of unexpected errors requiring reboots and reinstallations. The issues aren’t just a minor inconvenience—they’ve cost me hours of valuable time.

While this frustration is mostly due to a [code 18](https://www.netlingo.com/word/code-18.php#:~:text=Refers%20to%20an%20error%20made,was%20working%20on%20yesterday%20morning%3F), I will document my struggles and hopeful fix.

## Probable Cause : Admin Permissions

One of the most aggravating aspects of the problem stems from how my work account is set up. Every program, including Docker, must be installed with admin privileges. Switching between my work account and the so-called “high privileges” admin account is a constant source of errors. The problem is probably not with Docker per se, but with the interplay between Docker, WSL, and the modified system paths imposed by my work environment. My non-admin account has a default root path of `Z:`, which further complicates matters.


Running the following commands revealed some disparities:

```bash
wsl --list --verbose
```

- **Admin Account:**
    ```bash
      NAME              STATE           VERSION
    * Ubuntu            Running         2
      docker-desktop    Stopped         2
```
    
- **Normal Account:**
    ```bash
      NAME              STATE           VERSION
    * Ubuntu            Stopped         2
      docker-desktop    Uninstalling    2
```
    

Notice how `docker-desktop` is marked as “Uninstalling” under the normal account. This discrepancy points towards the underlying issue.

## The Road to Resolution

After countless trials, one solution finally began to make sense. I decided to execute:

```bash
wsl --shutdown
```

followed by:

```bash
wsl --unregister docker-desktop
```

I ran these commands from both the admin and normal user accounts and restarted Docker Desktop. Remarkably, this cleared the path for Docker to start normally. The act of unregistering the problematic `docker-desktop` distribution appears to have reset Docker’s internal state, allowing it to bypass the issues caused by the conflicting environment setups.



If the above does not work, we can simply use the following commands to force kill the processes : 
```bash
taskkill /F /IM wsl.exe
taskkill /F /IM vmmem.exe
```



