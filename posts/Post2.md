---
title: What Does a Craft Community Hub Actually Need to Do?
date: 2026-04-21
author: Lydia Kong
summary: Thinking through the functional requirements for a craft project tracking community - what's essential, what's optional, and what I'm cutting.
tags:
  - functional requirements
  - craft
  - planning
---

Last week I settled on the general idea - a community hub for craft hobbyists, built around project logging rather than just photo sharing. This week I want to get more specific about what that actually means in terms of features and data.

## Who is this for?
People who do slow, tactile hobbies for example, jigsaw puzzles, bead art, embroidery, cross stitch, crochet, that kind of thing. What these communities share is that projects take time, sometimes weeks, and the satisfaction comes from the process as much as the finished result. Most existing platforms (Reddit, Instagram, Rednote) only really support the finished product. I want to build something that values the in-between.

## Core functional requirements
**Essential:**
- Users can create a project: name, craft type (from a set of categories), difficulty level, and status (not started / in progress / completed)
- Users can add timestamped progress updates to an existing project
- The community can browse a feed of recently updated projects

**Nice to have if time allows:**
- Filter or search by craft type or status
- A simple stats view: projects completed, most active craft type

## What I'm not building
Image uploads. The brief is actually explicit about this - prototypes don't need to recreate standard platform features like photo uploads, which are assumed to be handled at the BlaBla Corp level. That makes this a brief-justified cut, not just a complexity trade-off. The value of a project log comes from the structured data anyway: progress over time, difficulty ratings, craft categories. That's what makes it different from posting a finished photo on Instagram.

## Data model
Two tables cover the core:

```sql
-- one project per user per craft project
projects (project_id, user_id, name, craft_type, difficulty, status, created_at)

-- many notes per project
progress_notes (note_id, project_id, content, created_at)
```

The one-to-many relationship between `projects` and `progress_notes` maps cleanly to MojoJS routes - one route to create a project, one to append a note, one to render the community feed. SQLite handles this structure well and I want to avoid over-engineering into something that needs complex joins just to function.

## What I'm still working out
How users navigate between their own projects and the community feed. There's a real question of whether "my projects" and "all projects" are the same view filtered differently, or two separate pages with different purposes. That decision affects how I structure the routes and templates, so I want to think it through before building anything.

One other thing worth flagging early: project entries should only be editable by their owner. The feed is public to all logged-in users, but write access needs to be scoped to the user_id from the session cookie. That's a basic data access constraint, but it's the kind of thing that's easier to build in from the start than to retrofit.