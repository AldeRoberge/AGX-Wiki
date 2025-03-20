I have been fighting, and losing, a war against Docker.

Docker is amazing. The idea, the concept of containerizing your apps, is great. I am fully on board with the principle.

But when it comes to the execution, I have been burned so badly. Unexpected errors, countless reboots, and reinstallations. I have tried Podman, which also suffered from issues. I have lost about 10 hours trying to get Docker to work.

In truth, it works 50% of the time. 50% of the time, I'm able to use it and it works very well as intended. But the rest of the time, it fails unexpectedly.

I'm using Docker for my job's work, which uses .NET Aspire. I'm also using it for personal and self-hosted shenanigans.

I'M 99% sure the problem lies in how my work account is set up. Every program must be installed with admin privileges. This switch between my work account and my admin account (they call it 'high privileges').

As an example, I'm currently getting this error : 

```
deploying WSL2 distributions
terminating WSL distro "docker-desktop": running WSL command wsl.exe C:\WINDOWS\System32\wsl.exe --terminate docker-desktop: Il n’existe aucune distribution avec le nom fourni.
Code d’erreur : Wsl/Service/WSL_E_DISTRO_NOT_FOUND
: running WSL command wsl.exe C:\WINDOWS\System32\wsl.exe --terminate docker-desktop: Il n’existe aucune distribution avec le nom fourni.
Code d’erreur : Wsl/Service/WSL_E_DISTRO_NOT_FOUND
: WSL distro not found error
checking if isocache exists: CreateFile \\wsl$\docker-desktop-data\isocache\: The network name cannot be found.
```


I have tried various combinations of installing as admin but launchin as normal user, running as admin user, using Docker Desktop as admin, etc.

I think another problem stems that the 'root' path of the non admin user is Z:
I don't know why, but my work's admins decided it was a good idea to change the default root path.

This leads to some stinking errors like : 

```
Failed to translate Z:\
```

What I'm attempting now : 

Using 

```
wsl --shutdown
```

And rebooting.