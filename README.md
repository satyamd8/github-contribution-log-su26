# Contribution [#1]: Admin Notification Table Styling (teammates)

**Contribution Number:** [**1** / 2 / 3]  
**Student:** Satyam Dhar  
**Issue:** [GitHub issue link](https://github.com/TEAMMATES/teammates/issues/13469)  
**Status:** Phase IV **Complete**

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
3. [Observed result] - The entire table has a light green background color (only on the first build).

### Reproduction Evidence

- **Commit showing reproduction:** https://github.com/satyamd8/teammates
- **Screenshots/logs:** <img width="1621" height="513" alt="image" src="https://github.com/user-attachments/assets/ede09f3a-500b-4fc9-9329-fccfcc3bc3b3" /> <img width="1601" height="515" alt="image" src="https://github.com/user-attachments/assets/b4a4673f-7399-4dbb-8802-771a9aa0754c" />


- **My findings:** [What you discovered during reproduction]
 Unlike the first screenshot in the issue, the entire table has a light green background color indicating a newly created notification. On a second build, the table returned to the normal transparent background color. Issue still exists as the style column isn't colored. 
---

## Solution Approach

### Analysis

From the styling, it seems to be an issue with Bootstrap and how certain styling classes are applied to the cells, aka the td elements. The Bootstrap "alert alert" class is being applied directly to the table cell even though it's meant for block elements. 

### Proposed Solution

The fix is fairly simple, since the alert alert class only applies to block elements, then we have to create a block elements. I can add a div or span inside of the td element thats specifically designated for the notification style. I can then transfer the Bootstrap classes from the td down to the block element that I use.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** The Bootstrap "alert alert" class is beign applied to the td table cell element, which doesn't do anything since the class only applies to block elements in HTML.

**Match:** In the same file and table, other td (table cell), tr (table row), and th (table header) elements have Bootstrap classes applied directly to them instead of a inner-nested block element. 

**Plan:** [Step-by-step implementation plan]
1. Add a div or other block element nested inside the td element that corresponds to the notification style column. 
2. Remove the existing Bootstrap "alert alert" class from thr td element. 
3. Transfer the Bootstrap classes to the div that's nested inside the td.

**Implement:** https://github.com/satyamd8/teammates/commit/dd82abf81549d1e7ae30069fc87fc4c5e8171cc2

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]
- Followed correct commit message format
- Didn't change the vision of the styling, followed the guidelines of the expected solution

**Evaluate:** I'll verify by checking the local environment again, and going to the /web/admin/notifications route to ensure the table cell styling is correct

---

## Testing Strategy

### Unit Tests

- [x] Test case 1: Verified that notification styling rendered as an alert div with the correct Bootstrap class rather than its own element
- [x] Test case 2: Verified that the alert Bootstrap styling is applied to the div, transferred from the td element
- [x] Test case 3: Verified that the notification style description text is correctly displayed inside the alert div

### Snapshot Tests

- Updated 2 failed snapshots in notifications-table.component.spec.ts to reflect the new HTML structure (alert div wrapped inside td instead of alert classes on td)
- Snapshots updated using Vitest watch mode (npm run test → press u to auto-update)
- Verified that only the intended structure changes appeared in snapshots after update

### Integration Tests

- [x] Verified that the notification table is rendered correctly with multiple notification types and their respective alert styles/colors.

### Manual Testing

[What you tested manually and results]

I manually tested the notification table and the styling through my browser in my private local environment of Teammates. I successfully confirmed that the notification styles displayed their correct colors, that the alert styling wasn't interfering with the table layout, and that all spacing, alignment, and styling was correct. 

---

## Implementation Notes

### Week [2] Progress

- I refactored notifications table style cell to use a div class="alert alert-..." wrapper instead of applying alert classes directly to the <td> element, which initially wasn't applying the correct style at all since alert classes only work on block elements. 
- This fixes the Bootstrap 5.3.0 compatibility issue where alert classes on table cells produced undefined styling behavior
- I verified on my local environment that the changes matched the expected solution outlined by one of the maintainers in the original issue thread. 

### Week [3] Progress

- I ran into an issue when running the codebases tets suite, which included both unit component tests and snapshot tests that tested individual frontend components and rendered snapshots against stored snapshots.
- One of the issues was incorrect formatting within the HTML, which was fixed through applying formatting through VSCode's Prettier extension.
- Another issue was that I was failing the snapshot tests that checked the notification table, so when running the tests in Vitest mode, I had to auto-update the snapshots to pass those tests. 

### Code Changes

- **Files modified:** notifications-table.component.html, notifications-table.component.spec.ts.snap
- **Key commits:** https://github.com/TEAMMATES/teammates/commit/b9b2315b0c2c4420b43f7baafa4a432321f05b8d
- **Approach decisions:** I intentionally chose to make the simple fix and transfer the alert classes from the original table cell that it was beign applied to, to a new div that would be nested inside the table cell. I did this to folow the guidelines of the expected solution that were outlined by a maintainer in the original issue thread, as many users that had submitted PRs before ended up changing the original styling of the whole table cell. 

---

## Pull Request

**PR Link:** https://github.com/TEAMMATES/teammates/pull/14140

**PR Description:** 
Fixes #13469 Admin Notification Page: broken styling on style column
Outline of Solution:
The issue occurred due to the Bootstrap "alert alert-*" class being applied to the table cell element instead of a block element. This was fixed by adding a div nested inside the td element, and transferring the Bootstrap class to that div instead, following the guidelines of the expected solution.

**Maintainer Feedback:**
- 6/8: Maintainer requested for screenshots showing the change in the PR description.
- 6/8: I immediately included the before and after screenshots in the description.

**Status:**  **Merged**

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]
- An important technical skill I learned was how to navigate through unfamiliar codebases, and single out the specific directories and/or files that I need to modify for a specific issue. When I first forked the repo, there were stacks and stacks of folders and files to look through just in the frontend. By identifying the different properties of the specific issue (notification table, admin page) along with using AI to help locate directories, I was able to find the specific frontend files that corresponded to my issue.
- Another important technical skill I learned was how to handle Pull Requests on GitHub and the steps I have to take before making changes and submitting a request. There were quite a few steps that were outlined by the maintainers to follow for anyone submitting a PR, so I had to make sure to read the documentation and follow the steps and not blindly submit a PR. 

### Challenges Overcome

[What was hard and how you solved it]
-  One big challenge I faced was trying to pass the automatic tests that were deployed when opening the Pull Request. There were a few different component tests and snapshots that kept failing, so I had to read through the developer documentation extensively to find out more about these tests. From that, I was able to run the tests on my local environment and single out the issues that caused the tests to fail. 

### What I'd Do Differently Next Time

[Reflection on your process]
- Next time I'll make sure to fully read through all parts of the developer documentation that correspond to the specific issue that I'm resolving, along with any information on Pull Requests and contributions. I didn't fully do that for this issue, which led to a slight delay in getting my PR accepted since I hadn't included all the necessary information. 

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
