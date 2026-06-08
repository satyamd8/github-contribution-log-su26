# Contribution [#]: Admin Notification Table Styling (teammates)

**Contribution Number:** [1 / 2 / 3]  
**Student:** Satyam Dhar  
**Issue:** [GitHub issue link](https://github.com/TEAMMATES/teammates/issues/13469)  
**Status:** [Phase I / **Phase II** / Phase III / Phase IV] [In Progress / Complete]

---

## Why I Chose This Issue

I chose to try to fix this issue because it aligns well with my strengths. A lot of my background is in Frontend development, as I've built and deployed multiple full-stack web apps. I've spent a lot of time working with and designing user interfaces and consistent layouts, and this specific issue seems like a basic UI/styling inconsistency that I can fix. The expected solution details also seem fairly well outlined which many contributors have not been able to meet. From this I hope to learn what kinds of issues may arise when updating frameworks/libraries, as it seems this issue occurred due to the codebase upgrading their Bootstrap version. I've never personally encountered such issues when upgrading libraries, so I'm curious to see what comes with it. 

---

## Understanding the Issue

### Problem Description

In the admin notification page, there's a table to modify the attributes of certain notifications. Under the Style column, the individual cells have transparent backgrounds instead of colored. 

### Expected Behavior

The individual cells should have color-coded backgrounds, corresponding to the color specified in the text, serving as a preview for the admin to see what the notification would look like for users.

### Current Behavior

The cells just have a transparent background color, only showing the text of the color/style. 

### Affected Components

The admin notification page and notification component Angular files are the only ones affected: 
admin-notifications-page.component.html
admin-notifications-page.component.ts
notifications-table.component.html
notification-style-class.pipe.ts
notifications-table.component.scss

---

## Reproduction Process

### Environment Setup

The steps to setup the environment are very simple, as they're clearly outlined in the teammates developer documentation. You must first fork the repo, clone the fork, and add the main repo as a remote and fetch all the updates. Make sure to have Java JDK 21, Node.js (minimum version 24), and Docker installed. You must then generate the config files and frontend dependencies. To start the local application, you start the docker database, apply the migrations, and start the backend and frontend servers. You can then create test accounts by logging in as an admin and creating instructor accounts to access all features.
The hiccups I ran in to occurred when I tried to access the admin page. These happened due to issues with the database migration, which was resolved by redoing the migration.

### Steps to Reproduce

1. Follow the steps to head to the admin login page and login as a test admin.
2. Go to the /web/admin/notifications route and create new notifications.
3. [Observed result] - The entire table has a light green background color.

### Reproduction Evidence

- **Commit showing reproduction:** https://github.com/satyamd8/teammates
- **Screenshots/logs:** <img width="1621" height="513" alt="image" src="https://github.com/user-attachments/assets/ede09f3a-500b-4fc9-9329-fccfcc3bc3b3" />

- **My findings:** [What you discovered during reproduction]
 Unlike the screenshot in the issue, the entire table has a light green background color. Issue still exists as the style column isn't colored. I wonder if the green is intentional, from an update that occurred after the issue was created, or if it's a bug that I'm running in to. 
---

## Solution Approach

### Analysis

[Your analysis of the root cause - what's causing the issue?]

### Proposed Solution

[High-level description of your fix approach]

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** [Restate the problem]

**Match:** [What similar patterns/solutions exist in the codebase?]

**Plan:** [Step-by-step implementation plan]
1. [Modify file X to do Y]
2. [Add function Z]
3. [Update tests]

**Implement:** [Link to your branch/commits as you work]

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]

**Evaluate:** [How will you verify it works?]

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [X] Progress

[What you built this week, challenges faced, decisions made]

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** [List]
- **Key commits:** [Links to important commits]
- **Approach decisions:** [Why you chose certain approaches]

---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
