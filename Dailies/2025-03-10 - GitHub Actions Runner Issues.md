I am not getting my GitHub Actions runner, self hosted locally or GitHub hosted, to properly build my game.  
  
I think it comes down to the fact that the RAM size required to build an executable is above 17Gb, which is the limit for GitHub hosted runners.  
  
I am attempting as we speak to get the runners to work on my local machines, which I have 4 of :  
  
- [Kitchen desktop being the least powerful](<Below is your text, revised and formatted in Markdown with corrected typos and improved structure:

---

## GitHub Actions Runner Issues

I am not getting my GitHub Actions runner—whether self-hosted locally or GitHub-hosted—to properly build my game. I suspect the problem is that the RAM required to build the executable exceeds 17GB, which is the limit for GitHub-hosted runners.

I am currently attempting to get the runners to work on my local machines. I have four systems:

- **Kitchen Desktop** – the least powerful  
- **Server** – a perfectly fine i7-6K  
- **Laptop** – an i7 10th gen  
- **Main Desktop** – an i9-12K

I tried all four and encountered various errors, including:

- **Git LFS not being installed**  
  *Fix:* Install it on WSL.

- **Docker integration not working**  
  *Fix:* Enable it in Docker settings.

Also, I need to mention that I'm using a Windows runner, which is mandatory for IL2CPP builds for Windows (this is what I need to send to Steam and Itch.io).

I estimate I have invested about 10 hours (probably more) trying to get the CI part of CI/CD to work—this is my first time doing it. I believe the effort is worth it since CI/CD is an invaluable tool for rapid prototyping and continuous testing.

---

## Security Concerns

I must protect my GitHub account at all costs. This means being very strict about where it is logged in. Right now, it's logged in on multiple computers, so I should log out of the ones I don't need to avoid any potential issues.

---

## Source Backups

I think it would be a good idea to download and keep an offline copy of the source code in case a catastrophic failure occurs with my GitHub repositories.

---

## Wiki Notes & Open Source

On a side note, I believe it is beneficial to open source my thoughts so that people in the future can understand what it's like to develop a game of this magnitude on their own. This might even be useful when parsed through an LLM or advanced AI.

---

## Using Quartz as a Wiki

Quartz is perfectly fine for a basic wiki, but I anticipate that eventually I will need a more advanced solution that supports localization, interactivity, embedded content, integrations, and accessibility. At the moment, no better alternative comes to mind.

It might also be a good idea to separate personal notes from the official game documentation, as currently everything is mixed together.

---

## Logo Considerations

I'm not too sure about the current logo—it’s a skull in red, black, and white. I feel I can do better, but I’m not certain. This is just a seed of an idea; I'm still rambling.

---

## Login Issues

Currently, login is broken due to a faulty, empty response from the server. This bug is linked to a more structural problem with the web server, which uses an outdated method for handling requests and responses. I believe I could improve this by using ASP.NET Core or even FastEndpoints (FE). I tried FE in the past; it was pretty nice, although it has some quirks.

---

## API 32 No Longer Supported

This is a real bummer since it's my girlfriend's Android version on the phone she currently uses. I understand it’s related to security and compatibility, but given how mature Android is, I expected support for older phones to continue for longer. It seems my girlfriend will need to get a new phone.

---

## About Apple

I have paid for my Apple developer license fee (\$100), but I still lack the following to push an iOS build:

- Time  
- A Mac with XCode  
- An iOS device for testing

My coworkers have iPhones, and I have promised them that they'll be able to play the game soon™

---

## About Microsoft Fees

I received a bill for \$60 for Microsoft services. I was on its free Azure plan—free isn't free anymore. I'll stick to my \$5 Hostinger VPS instead. Thanks, Microsoft.

---

## Screen Loading Time

I have tried to optimize the app's load time as much as possible, but I wish the splash screen loaded faster. I can't do much about it, though I really hope to reduce it to a maximum of 1–2 seconds.

---

## Time Constraints

There is very little free time for me to work on the game these days. I have about one hour each evening, which isn’t enough to start any meaningful task. I find myself stuck in planning hell, constantly adjusting what needs to be done without making significant progress.

When I work late at night, the following morning is challenging; I spend about 30 minutes recovering from a lethargic state and caffeine withdrawal. Even during dinner, I only have about 20 minutes of free time, often spent scrolling through Facebook (which I try to avoid as it is mindless and unproductive). I also try to steer clear of Instagram, TikTok, X, and Reddit for similar reasons.

After work, I prepare dinner and do various chores, and by the time I sit down to eat, it’s already late. If I could find efficiency during the day, I would split tasks into very tiny 15-minute chunks that can be paused and resumed.

There are many great AI task management tools (e.g., Monday, Notion, ClickUp), but they are all paid, and I’m already way over budget on this project.

---

## Budget Constraints

What started as a \$0 budget has turned into thousands of dollars spent on Unity assets, hosting fees, and various other costs—all from my own limited funds. I recently finished my master's degree with tens of thousands of dollars in student debt. A year later, I'm almost all repaid, but my resources remain very limited. With inflation, being frugal is even harder. I regret many Unity assets that turned out to be useless in the long run.

Both money and time are major constraints, which means the game is progressing at a snail's pace. Every day that passes, I worry that people will lose interest. Despite this, I value my ability to make a fun game, even though many AAA and indie studios are struggling or shutting down. People seem burnt out by the constant news and drama, leaving them with little desire to play.

I'm trying to figure out how to better spend my limited time. I've already made a conscious effort to minimize idle time, and I believe it comes down to two things:

- **Break tasks into bite-sized chunks** that can be paused and resumed at will.  
- **Find time in the early morning** rather than late at night.

Working late at night is great—the trance-like 3 AM coding clarity is unparalleled, almost like being on concentration drugs. However, when morning comes, it’s hard to transition, especially when a strict schedule is in place. Working in the morning has the advantage of a hard deadline: you must stop when the day starts, unlike at night when you can often push on.
