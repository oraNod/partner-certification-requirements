# Certification tooling

This section provides tooling recommendations and guidance for Ansible collection certification.

## Certification checker

The [partner-certification-checker](https://github.com/ansible-collections/partner-certification-checker) provides a GitHub Actions workflow that checks collections against certification requirements before you upload to Automation Hub

To start using it, copy the [certification workflow](https://github.com/ansible-collections/partner-certification-checker/blob/main/.github/workflows/certification.yml) to your `.github/workflows/` directory.

For complete instructions, see the [certification checker README](https://github.com/ansible-collections/partner-certification-checker/blob/main/README.md).

## Claude Code certification review

The [certification-review](https://github.com/ansible-collections/partner-certification-requirements/tree/main/.claude/skills/certification-review.md) skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) reviews Ansible collections against certification requirements interactively.

### Install the skill

Install the skill from this repository as a Claude Code plugin:

```shell
claude install-skill github:ansible-collections/partner-certification-requirements
```

### Run a certification review

Open your collection project directory in Claude Code and invoke the skill:

```
/certification-review
```

Claude fetches the current certification requirements, explores your collection, and checks each requirement one at a time.
At the end, it produces a summary table with a PASS or NEEDS ACTION status for each requirement area.
