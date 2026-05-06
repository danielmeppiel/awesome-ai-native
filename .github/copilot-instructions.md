Always validate approach with the user before changing any files. You MUST get explicit consent before modifying or creating files in the repository. The user will likely iterate with you and your approach until validating the final implementation.

# VSCode Agent Primitives

- VSCode already implements some Agent Primitives natively:

    - **Custom Agents**: Specialist personas with `.agent.md` files in the `.github/agents/` directory. Each Custom Agent has its own MCP tool boundaries and model configuration in the YAML frontmatter. Custom Agents replaced the legacy `.chatmode.md` files.
    - **Skills**: Reusable decision frameworks distributed as `SKILL.md` files (typically under `.github/skills/<name>/SKILL.md` or installed via APM into `apm_modules/`). Skills are the new entrypoint primitive — they activate on code patterns and can be summoned from a Custom Agent (or summon one).
    - **Instructions Files**: Modular instructions for context-specific guidance with the general `copilot-instructions.md` in the `.github` folder and `.instructions.md` files including `applyTo` patterns in the `.github/instructions` folder. They are automatically loaded based on the agent's context.
    - **Prompt Files**: Reusable task templates with `.prompt.md` files in the `.github/prompts` folder. Can be summoned with `/prompt` command in chat

- Ensure you fetch related documentation from the [VSCode Copilot Customization Guide](https://code.visualstudio.com/docs/copilot/copilot-customization) using the `fetch` MCP tool.

- Our framework should build on the way VSCode implements Agent Primitives. 

- When sharing implementation examples, they should conform as much as possible to the VSCode native, supported Agent Primitives structure and default paths, using `.agent.md`, `.instructions.md`, `.prompt.md`, and `SKILL.md` files as appropriate. 
    - IMPORTANT: However please note that in our framework we may extend to include more primitives or patterns that are not yet supported by VSCode natively. 
    - This is because we seek to build on top of what exists and yet push the boundaries of Agent Primitives to create a more powerful and flexible AI Native Development framework. This is frontier work.

- The site renders locally with jekyll at `http://localhost:4000/awesome-ai-native/`.