# My Favorite JQL Quries

### My Current Tickets without Estimates 
```JQL
Sprint in (openSprints()) AND "Story Points" is EMPTY AND assignee = currentUser()
```

### My Future Tickets without Estimates 
```JQL
Sprint in (futureSprints()) AND "Story Points" is EMPTY AND assignee = currentUser()
```

### Completed in last 24 Hours
```JQL
status changed to done after -1d  AND project in (projectsLeadByUser())
```

### Added in the last 24 Hours
```JQL
created >= -1d AND project in (projectsLeadByUser()) ORDER BY sprint ASC, created DESC
```

### Mentions Me
```JQL
(
  summary ~ currentUser() OR 
  description ~ currentUser() OR 
  comment ~ currentUser()
) AND 
status not in (Done, Deployed, Resolved, Closed) AND 
updatedDate >= -7d 
ORDER BY lastViewed ASC
```

### My Open Tasks -- JDS Kanban Board
```JQL
(
  status not in (Done, Deployed, Resolved, Closed, "Ready for Production") OR 
  updatedDate >= -7d
) AND 
( 
  assignee in (currentUser()) 
  OR project = "Jason Scanzoni Tasks" 
  OR (
    summary ~ currentUser() 
    OR description ~ currentUser() 
    OR comment ~ currentUser()
  ) AND 
  status not in (Done, Deployed, Resolved, Closed) AND 
  updatedDate >= -7d AND 
  Sprint in (openSprints())
) AND 
(
  sprint not in closedSprints() OR
  sprint is EMPTY
) AND 
issuetype != Epic AND 
(
  "Deployment Status" != "Ready for Production" OR 
  "Deployment Status" is EMPTY
) 
ORDER BY duedate ASC, priority DESC, updated ASC, createdDate ASC
```

![Screenshot of swimlanes in JIRA](https://github.com/jscanzoni/jql/blob/master/Swimlanes%20Configuration.png)
