(userguide)=
# User Guide

PR Pilot gives you a natural language interface for your Github projects. Given a prompt, it uses LLMs (Large Language Models) to autonomously interact with your code base and Github issues, enabling a wide variety of ground-breaking AI-assisted automation use cases.

This guide will help you understand how to use PR Pilot with your Github project.
## Installation

If you haven't done so, [install PR Pilot](https://github.com/apps/pr-pilot-ai/installations/new) into your repository.

## Where to Start

PR Pilot's "text-to-action" approach allows you to interact with your Github project using natural language via our [API](https://app.pr-pilot.ai/api/swagger-ui/).

![PR Pilot Architecture](img/overview.png)

Built on top of the API, PR Pilot offers a variety of tools and integrations to help you automate your Github project.
Which one is best for you highly depends on your specific use case. In our [blog](https://www.pr-pilot.ai/blog), 
we provide examples of how to use PR Pilot in different scenarios, for example:

- [Building a slash command for Slack](https://www.pr-pilot.ai/blog/a-natural-language-interface-between-slack-and-github)
- [LLM-assisted technical refinements for JIRA tickets](https://www.pr-pilot.ai/blog/a-jira-integration-for-llm-assisted-technical-refinements)
- [Creating Github Actions that interact with issues and PRs using natural language](https://www.pr-pilot.ai/blog/the-power-of-agentic-workflows)

You can use PR Pilot in different ways:

### Command-Line Interface
Our [CLI](https://github.com/PR-Pilot-AI/pr-pilot-cli) puts PR Pilot right at your fingertips:

```bash
pip install --upgrade pr-pilot-cli
```

Open a terminal and `ls` into a repository you have installed PR Pilot, then:

**📝 Ask PR Pilot to edit a local file for you:**

```bash
pilot --edit cli/cli.py "Make sure all functions and classes have docstrings."
```

**⚡ Generate code quickly and save it as a file:**

```bash
pilot -o test_utils.py --code "Write some unit tests for the utils.py file."
```

**🔍 Capture part of your screen and add it to a prompt:**

```bash
pilot -o component.html --code --snap "Write a Bootstrap5 component that looks like this."
```

**📊 Get an organized view of your Github issues:**

```bash
pilot "Find all open Github issues labeled as 'bug', categorize and prioritize them"
```

**📝 Generate parts of your documentation with a template:**

```bash
pilot --direct -f prompts/README.md.jinja2 -o README.md
```

For more examples, check out [template prompts](https://github.com/PR-Pilot-AI/pr-pilot-cli/tree/main/prompts).


### Python SDK

To use PR Pilot in your own tools and integrations, you can use the [Python SDK](https://github.com/PR-Pilot-AI/pr-pilot-python):

```bash
pip install pr-pilot
```

Use the `create_task`, `get_task` and `wait_for_result` functions to automate your Github project:

```python
from pr_pilot.util import create_task, wait_for_result

github_repo = "PR-Pilot-AI/pr-pilot"
task = create_task(github_repo, "Summarize the README file and create a Github issue with the result.")
result = wait_for_result(task)
print(result)
```

The Python SDK works great for creating [powerful Github Actions](https://github.com/PR-Pilot-AI/smart-actions).


### Using the REST API

The PR Pilot API allows you to trigger tasks using your own tools and integrations.

1. Create a new API Key in the PR Pilot [dashboard](https://app.pr-pilot.ai/dashboard/api-keys/).
2. Use the API Key to authenticate your requests to the [PR Pilot API](https://app.pr-pilot.ai/api/swagger-ui/).

Example:
```bash
curl -X POST 'https://app.pr-pilot.ai/api/tasks/' \
-H 'Content-Type: application/json' \
-H 'X-Api-Key: YOUR_API_KEY_HERE' \
-d '{
    "prompt": "Properly format the README.md and add emojis",
    "github_repo": "owner/repo"
}'
```

### Talk to the Agent in Github Comments

PR Pilot will create issues and PRs for you. To stay in the flow, just use the `/pilot` command followed by a description of the task you want to perform.


![First pilot command](img/first_command.png)

The bot will turn your comment into a link to your [dashboard](https://app.pr-pilot.ai), where you can monitor the task's progress.

### Smart Github Actions

If you're comfortable with Github Actions and want to create your own automations, you can use our **[Smart Actions](https://github.com/PR-Pilot-AI/smart-actions)** to create your own workflows.
These actions are hand-crafted using state-of-the-art prompt engineering techniques and let you automate your Github projects in powerful new ways.



## Monitoring Tasks

While a task is running, **PR Pilot** will create events that you can follow in the [dashboard](https://app.pr-pilot.ai/dashboard/tasks/):

![PR Pilot](img/how_it_works_dashboard.png)

You'll also get a detailed overview of how your credits were spent.

![Monitoring PR Pilot](img/how_it_works_cost.png)