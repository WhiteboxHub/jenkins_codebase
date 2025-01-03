# Jenkins Architecture

Jenkins follows the **Master-Agent** model:
- **Master**: Orchestrates jobs and pipelines.
- **Agent**: Executes tasks like building, testing, and deploying.

## Workflow:
1. Developers push code.
2. Jenkins triggers builds/tests.
3. Results (pass/fail) are shared.

This architecture allows for scalable builds and distributed work across multiple agents.