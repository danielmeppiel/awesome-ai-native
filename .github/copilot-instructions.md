Always validate approach with the user before changing any files. You MUST get explicit consent before modifying or creating files in the repository. The user will likely iterate with you and your approach until validating the final implementation.

# VSCode Agent Primitives

- VSCode already implements some Agent Primitives natively:

    - **Chat Modes**: Domain-specific chat behavior with `.chatmode.md` files. They have to be configured in the `.github/chatmodes/` directory. Each chat mode can have its own set of MCP tools and model configurations in the yaml frontmatter.
    - **Instructions Files**: Modular instructions for context-specific guidance with the general `copilot-instructions.md` in the `.github` folder and `.instructions.md` files including `applyTo` patterns in the `.github/instructions` folder. They are automatically loaded based on the agent's context.
    - **Prompt Files**: Reusable task templates with `.prompt.md` files in the `.github/prompts` folder. Can be summoned with `/prompt` command in chat

- Ensure you fetch related documentation from the [VSCode Copilot Customization Guide](https://code.visualstudio.com/docs/copilot/copilot-customization) using the `fetch` MCP tool.

- Our framework should build on the way VSCode implements Agent Primitives. 

- When sharing implementation examples, they should conform as much as possible to the VSCode native, supported Agent Primitives structure and default paths, using `.chatmode.md`, `.instructions.md`, and `.prompt.md` files as appropriate. 
    - IMPORTANT: However please note that in our framework we may extend to include more primitives or patterns that are not yet supported by VSCode natively. 
    - This is because we seek to build on top of what exists and yet push the boundaries of Agent Primitives to create a more powerful and flexible AI Native Development framework. This is frontier work.