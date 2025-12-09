# ADR-001: VLA Educational Content Architecture

> **Scope**: Document decision clusters, not individual technology choices. Group related decisions that work together (e.g., "Frontend Stack" not separate ADRs for framework, styling, deployment).

- **Status:** Accepted
- **Date:** 2025-12-08
- **Feature:** 001-vla
- **Context:** Need to establish an educational framework for Vision-Language-Action (VLA) models in the context of humanoid robotics that is accessible to beginners while maintaining technical accuracy. The approach must balance theoretical understanding with practical implementation examples, using appropriate tools and frameworks that enable reproducible learning experiences.

<!-- Significance checklist (ALL must be true to justify this ADR)
     1) Impact: Long-term consequence for architecture/platform/security?
     2) Alternatives: Multiple viable options considered with tradeoffs?
     3) Scope: Cross-cutting concern (not an isolated detail)?
     If any are false, prefer capturing as a PHR note instead of an ADR. -->

## Decision

- **Documentation Platform**: Docusaurus (static site generator with React-based components)
- **Content Format**: MDX (Markdown + JSX for interactive elements)
- **Programming Language**: Python 3.11+ for code examples and implementations
- **AI/ML Frameworks**: PyTorch, Transformers, Hugging Face for VLA model examples
- **Computer Vision**: OpenCV, NumPy, SciPy for vision processing components
- **Target Platform**: GitHub Pages for deployment and accessibility
- **Educational Structure**: Theoretical foundations → Practical examples → Real-world applications
- **Code Examples**: Beginner-friendly, reproducible on standard development environments

## Consequences

### Positive

- Docusaurus provides excellent search, versioning, and navigation features for educational content
- MDX allows embedding interactive elements and live code examples within documentation
- Python ecosystem has rich support for AI/ML and computer vision with extensive community
- GitHub Pages provides free, reliable hosting with version control integration
- Focus on reproducible examples ensures learners can follow along without complex setup
- Modular architecture allows for updates and improvements without breaking existing content

### Negative

- Python ecosystem can have complex dependency management for beginners
- Computational requirements for VLA models may be high for some learners
- Rapidly evolving field means some examples may become outdated quickly
- Limited interactivity compared to dedicated learning platforms
- Static site limitations for complex interactive demonstrations

## Alternatives Considered

Alternative Approach A: Jupyter Notebooks + GitHub/GitLab Pages
- Why rejected: Less suitable for structured textbook format, harder to maintain navigation and cross-references

Alternative Approach B: Interactive learning platform (e.g., CodeSandbox, Replit)
- Why rejected: More complex setup, less control over content, potential costs, dependency on third-party services

Alternative Approach C: Traditional PDF textbook format
- Why rejected: Limited interactivity, harder to update, less accessible for collaborative development

Alternative Approach D: Video-based learning with supplementary materials
- Why rejected: Less accessible for different learning styles, harder to search and reference specific content

## References

- Feature Spec: /specs/001-vla/spec.md
- Implementation Plan: /specs/001-vla/plan.md
- Related ADRs: none
- Evaluator Evidence: /history/prompts/001-vla/1-generate-vla-models-tasks.tasks.prompt.md