# Accessible Routing in Single-Page Applications

## The Problem

Single page applications made our apps faster, because we no longer had to reload all of the content every time, thanks to `pushState`. However, `pushState` purposefully came with no event hook, and the thinking was that developers should manually manage focus (the IRC logs from that time are in the reference repository, and we’ve spoken with some of the folks who were involved with the decision at that time). 

We could also respect the traditional URL, which made the experience feel like browsing on a static site- for all users except ones that need assistive technology.

There are well-known issues that users with assistive technology have when it comes to client-side routing: 

-	Because there is no full-page refresh, the user has no way of knowing that the page has changed at all. 
-	Because there is no focus management, the user’s focus remains where it is.
  o	In cases where the item that had focus goes away, focus is lost. 
  o	In the cases where the item that has focus doesn’t go away, the focus simply remains where it is (and if you imagine the user interacting with a link in the footer, and then they experience silence- and their focus still stays on that link in the footer- well, that’s a bad experience. Makes it feel like something is broken.

So we have two distinct issues: 
-	Lack of focus management
-	Lack of feedback that a page transition has occurred

## Current Solutions

From what I am aware of, current solutions use one or more methods to resolve the issue: 
-	Dynamically set the focus on a wrapper element
-	Dynamically set focus on a heading element (h1-h6) to move focus to the new content
-	Dynamically set focus to an interactive element such as a skip link
-	Use an aria-live region announcement
-	Imitate a traditional browser refresh by resetting focus

## Thinking About A Permanent Solutions
Of all the solutions I have researched over the past two years, there are two ideas that have presented themselves with more clarity, especially over the past few months.

1. Frameworks should provide an explicit node element or outlet where new content is inserted/replaced. This should differ from other outlet types, in that it receives focus when new content is added. 
2. A joint proposal for a new event hook should be explored- something that indicates that a semantic navigation event has occurred. Both frameworks and assistive technology could use this event to indicate/recognize new content. 

What do you think?
