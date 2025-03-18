
|**Field**|**Type**|**Description**|**Example**|
|---|---|---|---|
|**Title**|Text|A concise, imperative statement describing the task.|Create a table in the wiki to list different field types for a management software task.|
|**Description**|Text|Detailed explanation of the task, including background, purpose, and relevant context.|We need a structured way to document different field types in our management system for consistency.|
|**ID**|Unique Identifier|A unique ID for tracking this task (useful for Git, issue tracking, etc.).|AGX-1|
|**Impact**|Scale|Helps prioritize the task in planning. Higher impact means it contributes significantly to overall goals.|⚪⚪⚪⚪⚪ (Very high impact)|
|**Effort**|Scale|An estimate of the effort required to complete the task, considering complexity and time investment.|⚪⚪○○○ (Low effort)|
|**Priority**|High, Medium, Low|Indicates how urgent this task is relative to others.|**High**|
|**Owner/Assignee**|Text|The team member responsible for completing and ensuring the success of the task.|Aldé Roberge|
|**Due Date**|Date (YYYY-MM-DD)|The expected completion date or deadline for the task.|2025-03-20|
|**Roadmap**|Now (green), Next (yellow), Later (red), Not accepted (gray)|Indicates when this task is planned for execution.|**Now (green)**|
|**Status**|Not Started (gray), In Progress (yellow), Blocked (red), Done (green)|The current state of the task.|**In Progress (yellow)**|
|**Tags**|List of keywords|Labels that help group similar tasks for filtering and searching.|**Documentation, UI, Backend**|


This is inspired by how [Jira](https://jira.atlassian.com/) and [Monday.com](https://monday.com/) frontends show tasks to users. 


### How to define a good task title

| Verb         | Description                                | Example                                 |
| ------------ | ------------------------------------------ | --------------------------------------- |
| **Add**      | Introduce a new feature or functionality   | **Add** dark mode support               |
| **Improve**  | Enhance or optimize an existing feature    | **Improve** login page responsiveness   |
| **Fix**      | Resolve a bug or issue                     | **Fix** profile update validation error |
| **Refactor** | Restructure code without changing behavior | **Refactor** authentication module      |
| **Remove**   | Remove a feature that is no longer needed  | **Remove** old analytics module         |

### How to define a good task description

| Role            | Goal                                         | Benefit                                                        |
| --------------- | -------------------------------------------- | -------------------------------------------------------------- |
| **As a** player | **I want to** be able to use the chat button | **So that** I can communicate and socialize with other players |
