# Custom Agent Skills

Personal collection of [Agent Skills](https://agentskills.io) for GitHub Copilot CLI and other AI agents.

## Skills

- **git-commit-message** - Expert guidance for writing professional Git commit messages following industry best practices from [Chris Beams' guide](https://cbea.ms/git-commit/)
- **weekly-impact-summary** - Generate evidence-based weekly impact summaries focused on measurable business outcomes using WorkIQ integration

## Installation

To use these skills with GitHub Copilot CLI:

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/skills.git ~/repos/skills
   ```

2. Create symbolic links or junctions to the skills directory:
   
   **Windows (PowerShell):**
   ```powershell
   $skills = Get-ChildItem "$env:USERPROFILE\repos\skills\skills" -Directory
   foreach ($skill in $skills) {
       $target = $skill.FullName
       $link = "$env:USERPROFILE\.copilot\skills\$($skill.Name)"
       if (-not (Test-Path $link)) {
           cmd /c mklink /J "$link" "$target"
       }
   }
   ```

   **macOS/Linux:**
   ```bash
   for skill in ~/repos/skills/skills/*/; do
       skill_name=$(basename "$skill")
       ln -s "$skill" ~/.copilot/skills/"$skill_name"
   done
   ```

## About Agent Skills

Agent Skills are an [open standard](https://github.com/agentskills/agentskills) maintained by Anthropic for giving agents new capabilities and expertise. Skills are folders containing:

- `SKILL.md` (required) - Instructions with YAML frontmatter (name, description) and markdown body
- Optional bundled resources: scripts, references, and assets

## License

MIT
