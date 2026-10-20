# Skills



## Teory about skills
[Antropic tutorial about skills](https://agentskills.io/home)

### What agent is loading from skills?
https://agentskills.io/home#how-do-agent-skills-work

- At startup it loads the name and description.
- If task matches a skill's description, the agent read the full SKILL.md instruction into context

### Skills recommendations
- Keep your main `SKILL.md` under 500 lines
- Add relative paths fro the skill root e.g. `scripts/extract.py`
- Validate skill with `skills-ref validate ./my-skill`

### Best practises for skill creators
- Create skills based on:
    - real internal knowledge, style guides, runbooks, failures
    - hands-on task, reuseable pattern into a skill
- Refine with a real execution, even if it was passing execution etc
- Add what the agent lacks, omit what it knows (Avoid what pdf is. Write which tool use to extract text)

## How to add open source skills


## How to add private skills