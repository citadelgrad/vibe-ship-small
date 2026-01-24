# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.0] - 2026-01-23

### Added

- Two-solution approach for managing AI-generated PRs
  - **Solution 1: GitHub Spec Kit** - Automated slash commands for AI coding workflows
  - **Solution 2: Manual PRD/Spec Templates** - Human-driven planning with explicit control
- Comparison table to help teams choose the right approach
- New documentation:
  - `docs/visuals-and-diagrams.md` - C4 Model and Task Graphs guide
  - `docs/architecture-tools.md` - Alternative tools reference (LikeC4, D2, Structurizr, ADR tools, arc42, AI diagram generators)
- `.gitignore` file
- Strategy documentation for managing large PRs

### Changed

- Restructured README to present both solutions with clear guidance

## [0.1.0] - 2026-01-21

### Added

- Initial release
- Core workflow documentation for AI-assisted development
- PRD template (`templates/prd-template.md`)
- Spec template (`templates/spec-template.md`)
- PR example document for chatbot workflows feature (`pr-example-chatbot-workflows.md`)
- Repository structure documentation

[0.2.0]: https://github.com/citadelgrad/vibe-ship-small/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/citadelgrad/vibe-ship-small/releases/tag/v0.1.0
