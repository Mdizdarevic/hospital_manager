```markdown
---
name: User Story
about: A user-facing piece of functionality
labels: user-story
---

## Story
As a <role>, I want <goal>, so that <benefit>.

## Acceptance criteria
- [ ] Given ... when ... then ...
- [ ] ...

## Definition of Done
- [ ] All acceptance criteria are met
- [ ] Code is merged to `main` through a reviewed pull request
- [ ] Automated tests for this story are written and passing
- [ ] Manual test case (if any) is executed and documented
- [ ] Documentation / README updated where relevant

## Dependencies
Blocked by: #<issue number> (set it in the Relationships panel as well)

## Story Points
<value from the Lab 2 scale>
```

And a lighter template for tasks, `.github/ISSUE_TEMPLATE/task.md`:

```markdown
---
name: Task
about: An implementable unit of work within a User Story
labels: task
---

## Description
...

## Parent user story
#<issue number>

## Done when
- [ ] ...
```
