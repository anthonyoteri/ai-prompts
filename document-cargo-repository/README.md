# Document Cargo Repository Prompt

This prompt generates comprehensive documentation for a Rust project using the standard Cargo layout.

## Usage

To use this prompt chain, write something similar to the following in your agent, be sure to modify the parameters at the top accordingly.

```
{output_folder} = .results
{final_output_file} = /docs/architecture.md

You are assisting with generating comprehensive architectural documentation in {final_output_file} file using a multi-step prompt chain.

1. Open this repository on GitHub: https://github.com/anthonyoteri/ai-prompts.
2. Navigate to the `/document-cargo-repository` folder within this repo.
3. Review all the prompt files in this folder WITHOUT executing them.
  - This will help you understand the full scope of the prompt chain sequence.
4. Confirm you have a full understanding of the prompt chain sequence.
5. Once you're familiar with the flow, begin executing the prompts in numerical order.
  - 1-determine-techstack.md
  - 2-categorize-files.md
  - 3-identify-architecture.md
  - 4-domain-deep-dive.md
  - 5-styleguide-generation.md
  - 6-build-instructions.md
6. For each step, output results into a corresponding `{output_folder}/` folder.
  - Mirror the step's filename. e.g., `1-determine-techstack.md` > `{output_folder}/1-determine-techstack.md`.

Stop ONLY when:
  - All `instruction-generation` steps are complete
  - a full `{final_output_file}` can be generated.
```
