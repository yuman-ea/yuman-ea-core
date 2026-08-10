# yuman-ea

**yuman-ea** is an open source framework for Enterprise Architecture (EA), built around a suite of AI agents and skills that assist EA practitioners across:

- **Business Architecture** — capability mapping, value streams, operating model analysis
- **Technology Architecture** — reference architectures, tech radar / rationalization, standards compliance
- **Portfolio Management** — application and project portfolio analysis, roadmapping, investment prioritization

The goal is to give EA teams a modular, extensible set of agents that can be composed into real EA workflows — reducing the manual overhead of artifact creation, analysis, and governance so architects can focus on decisions rather than documentation.

## Why yuman-ea

Enterprise Architecture work is broad and repetitive: stakeholder interviews, capability models, tech assessments, portfolio reviews, and governance artifacts all follow recognizable patterns. yuman-ea packages these patterns as reusable, composable AI agents and skills, so any team can plug them into their own EA practice instead of building from scratch.

## What's inside

- **Agents** — task-oriented AI agents for specific EA activities (e.g., capability model generation, TCO/portfolio analysis, architecture review assistance)
- **Skills** — reusable building blocks (templates, prompts, evaluation criteria, frameworks) that agents draw on and that can also be used standalone
- **Framework** — shared conventions and interfaces so agents/skills compose predictably

> This project is in early stages. Structure and APIs are expected to evolve — see [open issues](../../issues) for current direction.

## Getting started

```bash
git clone https://github.com/<org>/yuman-ea.git
cd yuman-ea
```

Setup and usage instructions will be added as the initial agent/skill set lands. Track progress in [Issues](../../issues) and [Discussions](../../discussions).

## Roadmap

- [ ] Define core agent/skill interface conventions
- [ ] Ship first Business Architecture agent
- [ ] Ship first Technology Architecture agent
- [ ] Ship first Portfolio Management agent
- [ ] Publish contribution templates for new agents/skills

## Contributing

Contributions are welcome — see [CONTRIBUTING.md](./CONTRIBUTING.md) for how to propose new agents/skills, coding conventions, and the PR process. Please also review our [Code of Conduct](./CODE_OF_CONDUCT.md).

## License

MIT — see [LICENSE](./LICENSE).

## Maintainers

Maintained by [@vvjcoder](https://github.com/vvjcoder) and co-maintainers. Reach out via GitHub Issues or Discussions.
