# Agent Hooks Example

[![Build status](https://badge.buildkite.com/fa1773bc74e3b4c38f6ecd29f32f714d153ced0dbd94b89ad9.svg?branch=main)](https://buildkite.com/buildkite/agent-hooks-example)
[![Add to Buildkite](https://img.shields.io/badge/Add%20to%20Buildkite-14CC80)](https://buildkite.com/new)

Use Buildkite Agent hooks to control which teams may run pipelines on an agent or group of agents.

[Buildkite agents][agent] have access to a wide variety of [environment variables][env-vars] describing the job they should run. They also have [hooks], small scripts, which allow you to add behaviour to the job lifecycle. Combining these two features allows implementing controls like restricting which teams may run pipelines on an agent or stack of agents, providing opportunities for platform teams to govern how agents might be used by development teams using them to build and ship their code.

In this example we have an agent hook in [`agent/hooks/environment`](agent/hooks/environment) pre-installed using [agent hooks on hosted agents][hooks-hosted], but you can add hooks to any agent. They usually go in [the `/etc/buildkite-agent/hooks` directory][agent-hooks-path]. Agent stacks like the [elastic-ci-stack-for-aws] allow [configuring hooks][elastic-stack-hooks] for a fleet of agents.

The `environment` hook runs before the repository has been checked out, so can be used to intercept and enforce policies before a job begins in earnest. But there are many hooks. You might like a `post-command` hook to tidy up an agent after the job command has run. See the [full list of job hooks available][hooks-detail].

<a href="https://buildkite.com/buildkite/agent-hooks-example/builds/latest?branch=main">
  <img width="2400" alt="Screenshot of pipeline allowing team member" src=".buildkite/screenshot.png" />
</a>

<a href="https://buildkite.com/buildkite/agent-hooks-example/builds/latest?branch=rogue&state=failed">
  <img width="2400" alt="Screenshot of pipeline rejected non-team member" src=".buildkite/screenshot-rejected.png" />
</a>

See [more about the team hook in the docs][docs-team-hook], or try it yourself:

[![Add to Buildkite](https://buildkite.com/button.svg)](https://buildkite.com/new)

You'll also need to install this hook on your own agents:

[`agent/hooks/environment`](agent/hooks/environment)

Use a [dedicated queue][queues] if you are running other agents.

  [agent]: https://buildkite.com/docs/agent/v3
  [agent-hooks-path]: https://buildkite.com/docs/agent/v3/configuration#hooks-path
  [hooks]: https://buildkite.com/docs/agent/v3/hooks
  [hooks-detail]: https://buildkite.com/docs/agent/v3/hooks#job-lifecycle-hooks
  [hooks-hosted]: https://buildkite.com/docs/pipelines/hosted-agents/linux#agent-images-using-agent-hooks
  [env-vars]: https://buildkite.com/docs/agent/v3/environment-variables
  [elastic-ci-stack-for-aws]: https://github.com/buildkite/elastic-ci-stack-for-aws
  [elastic-stack-hooks]: https://buildkite.com/docs/agent/v3/aws/elastic-ci-stack/ec2-linux-and-windows/secrets-bucket
  [queues]: https://buildkite.com/docs/agent/v3/queues
  [docs-team-hook]: https://buildkite.com/docs/platform/team-management/permissions#manage-teams-and-permissions-programmatically-managing-teams

## License

See [LICENSE](LICENSE) (MIT)
