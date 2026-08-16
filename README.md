# yuman-ea

**An open source framework of AI agents and skills for Enterprise Architecture** — covering business architecture, technology architecture, and portfolio management.

## Mission — codify enterprise architecture

Enterprise architecture's methods live in consultants' heads, proprietary platforms, and expensive training. They are rarely written down, almost never inspectable, and impossible to improve collectively.

**Yuman EA writes them down** — as open, executable skills that state their criteria, their weightings, the data a decision actually requires, and the artifact it should produce. Any organization can run them, inspect them, argue with them, and override them for its own context.

The measure of success is a real decision improved: an architect who can walk into a steering committee with analysis that holds up.

Three commitments follow, and they constrain every design decision in this repository:

- **Work with the data teams actually have.** Skills declare what they need, what's optional, and what they do when it's missing — degrading honestly rather than demanding a complete CMDB before producing anything.
- **Produce output a non-specialist can defend.** Deliverables explain their reasoning in the language of the business, not the vocabulary of a framework. A user should never need to have read TOGAF to use, or defend, the result.
- **Always show the work.** Every recommendation ships with its assumptions, its confidence, and what would change the answer. Consultants win arguments partly by showing their reasoning; this framework does it by default.

## What's covered

- **Business Architecture** — capability mapping, value streams, operating model analysis
- **Technology Architecture** — build-vs-buy, reference architectures, technology lifecycle, standards conformance
- **Portfolio Management** — application rationalization, roadmapping, investment prioritization

## What's inside

- **Agents** — task-oriented AI agents for specific EA activities (e.g., capability model generation, TCO/portfolio analysis, architecture review assistance)
- **Skills** — reusable building blocks (templates, prompts, evaluation criteria, frameworks) that agents draw on and that can also be used standalone
- **Framework** — shared conventions and interfaces so agents/skills compose predictably

> This project is in early stages. Structure and APIs are expected to evolve — see [open issues](../../issues) for current direction.

## Getting started

```bash
git clone https://github.com/yuman-ea/yuman-ea-core.git
cd yuman-ea-core
```

Setup and usage instructions will be added as the initial agent/skill set lands. Track progress in [Issues](../../issues) and [Discussions](../../discussions).

## Roadmap

- [ ] Define core agent/skill interface conventions
- [ ] Ship first Business Architecture agent
- [ ] Ship first Technology Architecture agent
- [ ] Ship first Portfolio Management agent
- [ ] Publish contribution templates for new agents/skills

## Contributing

Contributions are welcome — see [CONTRIBUTING.md](./CONTRIBUTING.md) for how to propose new agents/skills, coding conventions, and the PR process. Please also review our [Code of Conduct](./CODE-OF-CONDUCT.md).

## License

Apache-2.0 — see [LICENSE](./LICENSE) and [NOTICE](./NOTICE).

Apache-2.0 was chosen for its explicit patent grant, which is the question enterprise legal review asks first. Contributions are covered automatically under §5, so there is no CLA to sign. Reasoning in [ADR-0003](./docs/adr/0003-license-apache-2.md).

## Maintainers

Maintained by [@vishaljavalkar-ai] [@rajesh-malviya] and co-maintainers. Reach out via GitHub Issues or Discussions.
