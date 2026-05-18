---
title: Finding My Group & Shifting Direction
date: 2026-04-24
author: Lydia Kong
summary: I paired up with a classmate this week and we agreed on a new concept - a community hub for pet owners dealing with separation anxiety.
tags:
  - groupwork
  - concept
  - planning
---

This week I sorted out my group situation. I paired up with my classmate Maggie, who had already been developing an idea around pet separation anxiety. After hearing her concept I thought it had real potential, so we decided to move forward together. That means shifting away from my original craft hub idea, which I still think was solid, but I also have similar experience with my own pets and the pet community direction felt more distinctive. It gave us a clearer standout feature to build around.

## The concept
A community hub for pet owners whose animals struggle with being left alone. It's a genuinely common problem. Dogs especially can become distressed or destructive when their owners leave, but most online resources are either too generic or scattered across forums with no structure. Our hub aims to fill that gap.

The core feature is a **case-matching system**: users input their pet's details and the system surfaces relevant cases that other community members have shared. Each case captures the problem, the routine or method the owner tried, and the outcome. Instead of scrolling through unrelated posts, you find experiences that actually mirror your situation.

## Who this is for
Pet owners, primarily dog owners though the concept extends to other animals, who are actively dealing with separation anxiety and looking for practical experience-based guidance. Not a vet diagnosis, just what worked for someone in a similar situation. That might be first-time owners, people returning to office work after working from home, or anyone whose pet developed anxiety after a life change.

## What makes it different
The value over a subreddit or Facebook group is the structured data behind each case. Because entries follow a consistent format, users can filter by pet type, behaviour pattern, or age group. An unstructured forum can't do that.

## Requirements taking shape
**Core:**
- Users can submit a case: pet type, age, behaviour description, method tried, outcome
- Users can browse and filter cases by pet type or behaviour category
- The matching view surfaces cases with similar pet profiles

**Optional:**
- Saving or bookmarking cases
- A follow-up field to update whether a method worked long-term

The data model is still early, but one table for cases is the starting point. The matching would work as a filtered query on pet type and behaviour, which should be manageable within SQLite. The submission form and the community feed would need to be handled as separate pages.

## Still to figure out
A lot of the interaction design is unresolved. The matching system sounds simple in principle but the UX of how users specify what they're looking for needs proper thought. I also want to make sure the case submission form is accessible and clearly labelled, because if the input is messy, the matching won't work.