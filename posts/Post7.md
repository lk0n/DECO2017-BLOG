---
title: Looking Back on Paws Alone
date: 2026-06-14
author: Lydia Kong
summary: A final reflection on how the Paws Alone prototype turned out once it was built and tested. What worked, what broke, and what I would change with more time.
tags:
  - reflection
  - evaluation
  - user experience
  - paws alone
---

This is the final post in the project. Earlier posts focused on planning the application: defining requirements and working out how the features would fit together. Now that Maggie and I have built and tested the prototype, I can look back at those decisions and evaluate how well they actually worked. To evaluate it we tested the key user flows, checked how the application behaved when things went wrong, and reviewed the interface against WCAG AA colour contrast requirements.

## How it performs
The parts that work do feel quick, but the feature the whole application depends on had a significant problem.

Saving advice is fast. We used HTMX for the save action, so the page updates without a full reload, and reading and writing through better-sqlite3 is quick enough at our scale that there was never a noticeable delay. Navigation between pages felt responsive throughout, and none of the core routes showed performance issues under normal use.

The biggest issue came from the Behaviour Check, which is the feature the application is built around. I could enter completely different combinations of pet type, behaviour, time alone, environment and stress level and still receive almost the same advice. The cause turned out to be more subtle than a simple bug. The matching function scores each advice case and returns the top six results, but we had only seeded six cases in total, so every search returned all six regardless of the input and only their order changed. Because some combinations produced tied scores, even the order often looked identical. The feature never crashed and always returned results, which is exactly why it was easy to miss. Functionally it worked, but it was not producing meaningfully different outcomes.

We also hit a smaller routing issue earlier, where the Submit Advice page returned a 404 error even though the page existed. Its route had never been registered; once it was added the page worked immediately. It was a simple fix, but it reinforced how dependent these applications are on the connections between components rather than the components themselves.

## What it is like to use
Navigation generally held up well. The active state in the navigation bar makes it clear which page you are on, and the Saved Plan page gives a useful empty state rather than a blank screen: if nothing has been saved, it explains why and directs you back to the Behaviour Check. Small details like this reduced dead ends and made the application feel more complete.

The Matches page also improved during development. Early versions displayed advice as a simple list, which made multiple results feel visually similar. Converting them into card based layouts made the content easier to scan and separated the pieces of advice from one another.

One thing I noticed while testing it myself was that not every action looks like an action. On one advice page I had left an important link styled as plain text rather than a button, so it blended into the surrounding content and was easy to overlook. It is a small example, but it shows how usability problems often come from presentation rather than functionality.

Accessibility was where evaluation revealed the clearest issues. Keyboard navigation works because we relied on standard links and form elements, the navigation bar includes a label for screen readers, and the body text, dark grey (#333) on a cream background (#FDF8F2), reaches about 12:1, comfortably above WCAG AA. The failures all came from the brand colours: white text on the orange header and buttons (#EC802B) only reaches about 2.7:1, and the teal used for tags and secondary links performs similarly poorly on white. These fail AA and would be hard to read for users with low vision. Encouragingly, this does not need a redesign. Using dark text on the orange elements and darkening the teal where it appears as text would resolve most of it while keeping the visual identity.

## What I would change, and why
The clearest issue I would fix took longer to identify than expected. Throughout development the application refused to adapt to smaller screens, with the header and content stuck at a desktop width. I assumed the problem was in the main stylesheet, but the cause was a min width of 1024px inside the animation stylesheet. One rule meant for a visual effect was quietly controlling the layout of the whole site. The fix was straightforward once we found it, but the lesson was about separation of concerns: a stylesheet meant for animation should not control layout, because when unrelated responsibilities mix, the cause of a problem ends up hidden somewhere unexpected.

The matching system would be my highest priority. It returns the top six results regardless of score, and with only six seeded cases that means everything is returned every time. Two changes would fix it: return fewer results or apply a minimum score threshold so irrelevant cases are excluded, and seed more cases so there are genuinely different options to choose from. Neither is difficult, but together they would make the feature far more useful. More structured testing would also have helped. If I had written a few example user profiles and decided what each should receive before building the matching, the problem would have shown up much earlier; instead I mostly tested whether the feature returned results, not whether they made sense.

The smaller improvements are still worthwhile: validation on the Submit Advice form to prevent empty submissions, styling every important action clearly as a button, and fixing the contrast issues found in testing. None are large on their own, but together they would make the application feel considerably more polished.

## Were our requirements right in the first place？
Looking back at the requirements from the planning phase, most were realistic and were delivered. The Behaviour Check, advice pages, saved care plan, community submissions and login all function as intended, and at a feature level the application broadly resembles what we set out to build.

What changed was my understanding of which requirements actually mattered. During planning I treated most features as equally important, and evaluation showed that was a mistake. The matching system was the core value of the application, because everything else depended on it producing relevant results. Community submissions and saved plans were useful additions, but only if matching worked first.

Testing also exposed a requirement missing from my original planning: validation. I spent a lot of time on what users should be able to do and very little on what should happen when they give incomplete or unexpected input, and the lack of validation on the Submit Advice form is a direct result. In hindsight I would treat matching quality, validation, accessibility and responsiveness as first class requirements from the start, rather than adding more features. Evaluation showed these mattered more to the usefulness of the application than several of the extras we built.

## Lessons learned
The biggest thing I learned is that a feature working is not the same as a feature being successful. It was easy to treat the absence of errors as evidence that something was finished, and the Behaviour Check showed why that is risky: it never crashed and always returned results, yet only testing revealed that different inputs produced almost identical outputs. I also became much more comfortable with routing, persistent data, HTMX, database design and debugging across multiple files. Most of our problems were not caused by complicated code but by small assumptions that went untested, and noticing that was probably the most useful lesson from the unit.

---

## Evidence

### Functional requirements: planned versus delivered
| Requirement (from planning) | Status | Notes |
|---|---|---|
| Behaviour Check form | Delivered | Collects pet type, behaviour, time alone, environment, stress level |
| Match advice to answers | Delivered, but flawed | Ran reliably but returned near identical results across different inputs |
| Advice detail pages | Delivered | Six seeded advice cases |
| Save advice to a care plan | Delivered | Persists to a `saved_advice` table |
| Saved Plan view | Delivered | Reads real saved items after an early hardcoded data bug |
| Submit Advice (community) | Delivered, under validated | No input validation or moderation |
| Login / logout | Delivered | Needed so a saved plan belongs to one user |

### Colour contrast against WCAG AA
AA requires a contrast ratio of at least 4.5:1 for normal text.

| Combination (where it appears) | Ratio | Result |
|---|---|---|
| Body text #333 on background #FDF8F2 | approx 12:1 | Pass |
| Card text #555 on white | approx 7.5:1 | Pass |
| White text on orange header and buttons #EC802B | approx 2.7:1 | Fail |
| Teal #66BCB4 card tags and back links on white | approx 2.2:1 | Fail |
| Orange #EC802B card title links on white | approx 2.7:1 | Fail |
| Suggested fix: dark text #333 on orange | approx 4.6:1 | Pass |

The body and card text pass comfortably. The failures all come from the same two brand colours used as foreground, either white on orange or orange and teal on white.