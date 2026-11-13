# Tool-to-Agent Comparison: Todoist → Claude with MCP

## Context

**Tool being replaced:** Todoist Premium (2024 version)  
**Agent being evaluated:** Claude 3.5 Sonnet with custom MCP server  
**Primary use case:** Managing development tasks, tracking blocked work, prioritizing daily work  
**Current usage:** 2 hours per day, ~40 tasks created per week, individual contributor  
**Evaluation period:** March 1 - March 30, 2026  

## Capability Comparison

### What the Tool Does

- Task creation with projects, labels, priorities, due dates  
- Recurring task templates  
- Task dependencies and blocking  
- Natural language date parsing  
- Mobile and desktop sync  

### What the Agent Does

- Task creation from conversational description  
- Automatic project inference from context  
- Priority suggestions based on calendar and past work  
- Daily briefing with blocked tasks highlighted  
- Rescheduling proposals when priorities shift  

### What Disappears

- Instant mobile access (agent requires terminal or web interface)  
- Guaranteed offline operation  
- Predefined recurring task templates  

### What Appears

- Automatic priority adjustment based on meeting notes  
- Task breakdown suggestions for large items  
- Detection of tasks blocked by missing context  

## Overhead Analysis

### Setup Cost

**Tool:**  
- Time to configure: 2 hours (projects, labels, filters)  
- Integrations required: 3 (calendar, email, Slack)  
- Documentation read: 1 hour  

**Agent:**  
- Initial instruction writing: 6 hours  
- Instruction iterations: 12  
- Context documents created: 4 (project definitions, priority rules, meeting schedule, blocked-task protocol)  
- Test runs until stable: 8  

### Ongoing Maintenance

**Tool (per week):**  
- Updates and fixes: 0.5 hours  
- User support: 0 hours  
- Integration maintenance: 0.2 hours  

**Agent (per week):**  
- Instruction refinement: 1 hour  
- Reviewing agent output: 3 hours  
- Handling agent failures: 0.8 hours  
- Coordinating agent handoffs: 0.5 hours (when agent escalates to human decision)  

## Performance Metrics

### Throughput

**Tool:**  
- Items processed per hour: 15 (manual entry)  
- Error rate: 2% (wrong project or priority)  
- Time blocked waiting: 0% (always available)  

**Agent:**  
- Items processed per hour: 25 (conversational batch creation)  
- Error rate: 8% (wrong project inference, missing priority)  
- Time idle waiting for human: 68% (measured from session logs)  
- Items requiring human review: 30% (priority confirmation, blocked-task escalation)  

### Context Requirements

**Tool:**  
- Context switching per task: Manual—I had to remember project and priority for each task  
- Knowledge required to operate: Basic task management concepts  

**Agent:**  
- Standing instructions written: 47  
- Context documents maintained: 4  
- Context check frequency: 3 per week (when projects or priorities changed)  

## Failure Mode Analysis

### Tool Failures

- Sync conflict (once per month): 5-minute resolution  
- Integration breakage (twice in six months): 30-minute resolution  
- Data loss: Never observed  

### Agent Failures

- Incorrect project inference (3-4 times per week): 2-minute correction  
- Blocked by missing context (once per week): 15-minute instruction update  
- MCP server timeout (once per week): 5-minute restart  
- Task duplication from misunderstood conversation (twice in 30 days): 10-minute cleanup  

### Blast Radius

**Tool:** Lost access to task list; could recover from mobile backup  
**Agent:** Lost task coordination; had to recreate context documents and re-verify agent state  

## Decision Criteria

### Scoring (1 = Tool Wins, 5 = Agent Wins)

| Criterion | Score | Weight | Notes |
|-----------|-------|--------|-------|
| Setup efficiency | 2 | 2 | Agent took 3x longer to reach stable operation |
| Ongoing overhead | 2 | 5 | Agent requires 5.3 hours/week vs 0.7 hours/week for tool |
| Throughput | 4 | 4 | Agent handles batch creation faster despite idle time |
| Reliability | 2 | 5 | 8% error rate vs 2%; more failure modes |
| Failure recovery | 3 | 3 | Tool recovers faster but agent failures easier to diagnose |
| New capabilities | 5 | 4 | Priority inference and blocked-task detection genuinely useful |
| Team learning curve | 3 | 1 | Only affects me; agent requires understanding its limits |

**Weighted Total:** 72  
**Maximum Possible:** 120  
**Percentage:** 60%  

### Interpretation

The 60% score puts this squarely in "trade-offs are mixed" territory. The agent wins on throughput and new capabilities, but loses on reliability and overhead. The decision depends on whether the new capabilities (priority inference, blocked-task detection) are worth the 4.6 extra hours per week of maintenance.

## What Actually Changed

### Work That Disappeared

- Manual project and priority assignment for each task  
- Daily review to find blocked tasks  
- Rescheduling when priorities shifted  

### Work That Appeared

- Writing and updating standing instructions  
- Reviewing agent output for incorrect inferences  
- Correcting agent mistakes (wrong project, duplicate tasks)  
- Updating context documents when projects or priorities changed  

### Role Shift

I moved from operating a task manager to managing an agent that operates a task manager. The agent handles more tasks per hour but requires constant verification. Instead of "add task, set priority, move on," the workflow became "describe work to agent, confirm it understood the context, review what it created." The cognitive load shifted from remembering details to teaching the agent my mental model.

## Decision

**Keeping:** Both (tool for mobile and offline; agent for conversational batch creation)  
**Reason:** The agent's priority inference and blocked-task detection are genuinely useful for planning work, but its 8% error rate and 68% idle time make it unreliable as the only system. The tool remains the source of truth; the agent drafts tasks that I confirm and sync back. This hybrid setup costs more overhead than either alone but avoids the agent's worst failure modes while keeping its best capabilities.  
**Next evaluation:** June 1, 2026  

## Lessons

- Agents work best when they draft, not decide—keep the tool as source of truth and let the agent propose changes  
- Idle time matters more than error rate—68% waiting for human input meant the agent's speed advantage disappeared in practice  
- Context documents decay fast—within two weeks, my project priorities had shifted enough to require instruction updates  
- New capabilities don't justify broken reliability—priority inference was useful but not worth the 8% error rate on basic task creation  
- Measure meta-work honestly—I spent more time teaching the agent than I saved from automation  
