---
title: Interpreting the Brief & Initial Idea
date: 2026-04-14
author: Lydia Kong
summary: Initial thoughts on the BlaBla Corp brief and why a craft and hobby community might be an interesting direction.
tags:
  - brief analysis
  - brainstorming
  - arts and crafts
  - planning
---

## Unpacking the brief
The **BlaBla Corp** brief asks us to build something that feels genuinely tailored to a specific community - not just a generic social feed. Reading it, I kept thinking: **what community do I actually understand well enough to design for?**

As someone who loves **arts and crafts**, I thought about people who do things like jigsaw puzzles, bead art, embroidery, or other slow, tactile hobbies. It's a niche that's grown a lot online but doesn't have a dedicated platform that takes it seriously.

## The core idea: a project log
The feature I'm most interested in exploring is a **project log** - a place where crafters can document progress, note materials used, and mark something as finished. What makes this interesting is that the data is actually structured, not just a post or a caption. An entry might look something like:

```text
project_name: "Cherry Blossom Cross Stitch"
craft_type: embroidery
status: completed
start_date: 2026-03-01
completion_date: 2026-04-05
notes: "Medium difficulty. Harder than expected."
```

## Core vs. optional
Here are some features I think are essential to have and ones that would be nice to include.

**Core (must work):**
- Users can create a project entry with title, craft type, and status (in progress / completed)
- Users can add timestamped progress notes to a project
- Completed projects appear in a community gallery view

**Optional (stretch goals):**
- Filtering or searching by craft type
- Community interaction beyond browsing (likes, comments)

## What I'm still working out
Two things I haven't resolved yet. First, whether craft type should be a **predefined list** or free-text. Predefined categories (embroidery, crochet, bead art etc.) make filtering and display much cleaner, but they also mean I'm deciding what counts as a valid craft type - which means they depend more on my assumptions rather than the users'. Free-text is more flexible but less useful for any kind of community browsing. I'm leaning toward a fixed list for now, with the acknowledgement that it might need expanding.

Second, how difficulty level works. Right now I'm thinking of it as a user-set label (easy / medium / hard), but that's entirely subjective. Two people could rate the same project completely differently. I'm not sure whether that makes it useless as a data field or just means it should be treated as personal context rather than something comparable across users.

Neither of these is a big issue, but I think they’re the kind of decisions worth noting at this early stage before actually starting to build.