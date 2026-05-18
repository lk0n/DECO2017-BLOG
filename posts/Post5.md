---
title: Scoping the Matching Feature
date: 2026-05-08
author: Lydia Kong
summary: Thinking through how the core matching feature should work, and deciding what's realistic to build within the scope of this project.
tags:
  - matching system
  - scope
  - technical decisions
---

After the data modelling work from last week, I've been sitting with one question: how does the matching actually work?

On the surface it seems simple. A user inputs their pet's details and gets back relevant cases. But when I started thinking about what "relevant" actually means, it got complicated. Does every detail need to match exactly? Does age need to be within a certain range? What if nothing matches at all?

## What I decided
For this prototype, the right call is to keep matching simple: filter cases by pet type, and optionally by behaviour tag.

The reason is straightforward. The more matching criteria we add, the more likely a user gets zero results. That's a worse experience than getting a few loosely relevant ones. A dog owner looking for help with barking should see all barking cases for dogs, not only the ones where the dog is also two years old and a specific breed.

The filtering would work as a query on pet type and behaviour tag. No ranking, no algorithm, just filtering. That feels achievable within the scope of this project.

## What we're not building
Any kind of relevance ranking. Sorting results by "closest match" would add a lot of complexity for unclear benefit at this stage. A working filter is more useful than a complicated recommender that might not work properly.

## What this means for the data model
It simplifies things slightly. Fields like pet temperament and alone time are still useful to display because they give context to the reader, but they don't need to drive the matching logic. The core filtering happens on pet type and behaviour tag, both already in our ERD.

## One thing still unresolved
Whether behaviour tags should be a fixed list or user-generated. A fixed list filters consistently but limits what users can express. User-generated tags are more flexible but messy. "Barking", "excessive barking", and "barks a lot" would all be treated as different tags. For a prototype, reliability matters more than flexibility, so I'm leaning toward a fixed list of around 8 to 10 common anxiety behaviours.

There's also an interface point worth thinking about: if tags are shown as selectable buttons, they need to work with keyboard navigation and meet colour contrast requirements. That's something to keep in mind when the frontend gets built.