# Trello Workflow

## Trello Board 

Trello board to have 4 states: backlog, in progress, test, done

![image](https://github.com/ossdhaval/mysite/assets/343411/13350d67-6732-4d6d-90a5-406193462e31)


## Creating new cards

- Add project label:
  - Epics and stories for a project are identified by a project label, for example `Terminal-cards` label. For every new module/project, a new card should be created. Each epic or story must have a project label. This is also how we can connect multiple stories of a project to its epic. You can filter on this project label to view overall status of the project
- Add epic-story-defect label:
  - Each card is either an `epic` or a `story` or a `defect`. Assign one of this label to the card. Any project can have only one epic labelled card.

## Tasks and Time tracking

- Each user-story should be broken down into tasks for front-end and back-end in different sections. Tasks should be small enough to be completed within a day. Everyday, a developer should be able to complete at least one task and update Trello accordingly.

## Communicating using Labels

- `Question` label
  - Use this label to indicate that developer has a question to be answered by product owner or technical lead.
  - When this label is used, the product owner will look into the card comments for a question from developer. Developer should ask detailed and well-explained question in the card comments.
- `Blocked` label:
  - Developer will apply this label to a card to highlight a need for urgent discussion or a question to be answered in order to make progress for that card.

## Defect workflow

- Cards with label `defect` will have the same life-cycle as `story` cards. Meaning, when a defect is created, it should be placed in the backlog and assigned to a developer. Developer picks it up and moves it to in-progress. When it is fixed, the developer will move it to test phase. Here, test engineer will retest it and move it either to completed state or back to backlog with relevant comments.
