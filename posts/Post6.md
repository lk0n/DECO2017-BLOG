---
title: Where We Are - Gaps, Decisions, and What's Coming Next
date: 2026-05-15
author: Lydia Kong
summary: Checking in on the current state of the project, what's been working, what still needs attention, and what we're building toward.
tags:
  - progress
  - planning
  - accessibility
---

With the data model and matching logic scoped out, I wanted to take stock of where the project actually stands before we move into building the prototype properly.

## What's holding up well
The data model feels solid. Having separate tables for cases, routines, and behaviour tags means the core matching feature is genuinely supported by the structure underneath it. It's not just a list of posts. The data is organised in a way that makes filtering possible without overcomplicating things.

The scope decision from the previous post has also stayed stable. Keeping matching simple rather than building a ranking algorithm was the right call. A working filter that reliably returns relevant cases is more useful than a sophisticated recommender that might return nothing or behave unpredictably.

## What still needs work
The Submit Case flow is the part I'm least confident about right now. Contributing to the community means filling in pet details, describing the problem, describing what was tried, and reporting the outcome. That's a lot of fields. I haven't thought carefully enough about how to make that feel manageable rather than overwhelming. If the submission experience is too heavy, people won't contribute cases, and without cases the matching feature has nothing to work with.

This is something we need to work through before building the form.

## Accessibility as a requirement, not an afterthought
The brief requires AA compliance, and this is the point where we need to be more aware and actively design for. 

The specific things that need proper attention as we build:

- Form field labelling on the case submission form for screen reader compatibility
- Colour contrast on behaviour tag badges
- Keyboard navigation through the case list and filter controls
- Clear communication of error states on form inputs

WCAG AA needs to be built in rather than added at the end. The brief is explicit about this, and it's also just good practice for a platform that handles community-submitted content.

## What's next
The next step is getting the core routes working in MojoJS: case submission, the community feed, and the filtered matching view. The data model is there, so the focus now is on connecting it to actual routes and templates, and making sure the user flow feels coherent when you move through the application rather than just on paper.

The Submit Case form design is the thing I want to get right before anything else.