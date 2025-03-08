---
title: Wiki
---
> [!warning] Advanced users
> 
> This guide is meant for users curious about the technical aspects and the process of editing and publishing the wiki. 
> To simply contribute changes to the wiki, we accept pull requests on the [AGX-Wiki](https://github.com/AldeRoberge/AGX-Wiki) GitHub.

The [AGX-Wiki](https://wiki.aliengarden.com/) is created from markdown notes edited in [Obsidian](https://obsidian.md/).

These notes are then converted into a static website using [Quartz](https://quartz.jzhao.xyz/), with a custom fork ([AGX-Wiki-Quartz](https://github.com/AldeRoberge/AGX-Wiki-Quartz)) handling fonts, icons, and styling.

The entire build and publishing process is automated using [Docker](https://www.docker.com/) and [Dockge](https://github.com/AldeRoberge/dockge).



#### Why Quartz?

In my process of making a wiki, I tried building my own wiki, [Fandom](https://www.fandom.com/), [Confluence](https://www.atlassian.com/software/confluence), , [OtterWiki](https://github.com/johw/otterwiki), [Wiki.js](https://js.wiki/), [YNAW](https://youneedawiki.com/), and many more. 

The AGX Wiki started as a [ClickUp Docs](https://clickup.com/features/docs) project, which is aesthetically pleasant, versatile, but has some limitations, including that is was slow, had no customizable branding on free plans and no public sharing with clean URLs. 

No solution came as close in terms of speed, looks, and cost as [Quartz](https://github.com/jackyzha0/quartz). I also tried [Perlite](https://github.com/secure-77/Perlite), which is really great too, but I found Quartz to be better overall.

While Obsidian [isn't open source](https://www.reddit.com/r/ObsidianMD/comments/1feojen/can_i_trust_obsidian_since_its_not_open_source/), it can easily be replaced by another markdown editor in case of classic almost inevitable [enshittification](https://www.wikiwand.com/en/articles/Enshittification).

#### Wiki hosting costs break down

Since writing a wiki is already a very time expensive endeavor, I didn't want the technical aspect to be too costly too. I tried to be as low budget as possible, and here is the cost break down :

| Component | Cost (per year, in CAD) |
| --------- | ----------------------- |
| Server    | $120                    |
| Domain    | $20                     |
| Wiki      | Free!                   |

