# Node 4 Implementation Plan

## Goal

Node 4 requires the selected VLN-related model to run independently as an offline inference demo before it is connected to the robot or the simulator control loop. The purpose of this stage is to verify that the model environment, dependencies, inputs, and outputs are all valid.

For this project, the most practical setup is:

- **Windows** as the main execution environment for model inference
- **Mac** as the supporting environment for documentation, experiment organization, prompt design, and result analysis

## Why Windows Is the Main Environment

The current project setup already places the simulation and the model environment on Windows. Since later stages such as Node 5 and Node 6 will depend on integrating model outputs with simulation or navigation components, it is more efficient to keep the Node 4 inference demo on the same machine. This avoids unnecessary cross-device debugging, file transfer friction, mismatched dependencies, and duplicated deployment work.

## Why Mac Is Still Useful

Although the main inference demo should run on Windows, the Mac environment remains useful for:

- maintaining literature notes and project documentation
- defining input and output formats for the model
- writing prompt templates and test instruction sets
- preparing experiment records and demo descriptions
- organizing logs and summarizing results after Windows-side runs

## Recommended Division of Work

### Windows Responsibilities

- Install and verify the selected model runtime environment
- Run the offline inference demo
- Check that the model can accept natural-language commands and produce stable outputs
- Save sample outputs, screenshots, and terminal logs
- Prepare the executable demo script for Node 4

### Mac Responsibilities

- Maintain the repository documentation for Node 4
- Draft the prompt format and structured output format
- Prepare the instruction test set for offline evaluation
- Organize experimental observations and conclusions into logs and reports
- Keep Obsidian notes synchronized with the repository progress

## Recommended Node 4 Deliverables

The minimum deliverables for Node 4 should be:

1. A working demo script on Windows that runs the selected model independently.
2. A short environment description explaining how the model was launched.
3. Example input instructions and example outputs.
4. A clear structured output format that can later support Node 5 integration.
5. A log entry and short write-up summarizing whether inference succeeded.

## Suggested Input-Output Design

At this stage, the output should already be constrained into a format that is useful for later navigation integration. Instead of allowing the model to return unrestricted free-form text, it is better to enforce a structure such as:

```json
{
  "target_object": "red box shelf",
  "landmark": "left storage area",
  "goal_description": "the shelf with red boxes near the loading corner",
  "action_hint": "move forward and turn left"
}
```

This format does not yet need to produce final Nav2-compatible coordinates, but it should already provide enough semantic information for the Node 5 bridge design.

## Node 4 Execution Steps

1. Finalize the selected backbone direction.
   For this repository, the preferred practical direction is a modular language-to-goal pipeline inspired by LM-Nav rather than a benchmark-only discrete VLN agent.

2. Prepare the Windows inference environment.
   Confirm that the model runtime, weights, dependencies, and command-line execution all work.

3. Build a minimal offline demo script.
   The script should take one natural-language instruction as input and return one structured inference result as output.

4. Prepare a small test instruction set.
   At least 10 navigation-style commands should be prepared in advance so that the model can be tested consistently.

5. Record outputs and failure cases.
   Save both successful and unsuccessful examples, because these will later help with Node 5 interface design and Node 6 evaluation.

6. Write the Node 4 summary.
   The final write-up should explain what was run, what the model accepted as input, what it returned as output, and what still needs to be connected in later milestones.

## Immediate Next Actions

The next practical actions are:

- On Windows: run the first standalone inference demo and save the output
- On Mac: prepare the instruction list and the expected output schema
- In the repository: add a Node 4 result log once the first inference run succeeds

## Success Criteria

Node 4 should be considered complete when:

- the selected model runs successfully on Windows
- at least one offline inference demo completes end to end
- the input and output format are documented clearly
- the output is structured enough to support the future Node 5 bridge

At this stage, the model does **not** need to control the robot or simulation directly. That integration belongs to the next milestone.
