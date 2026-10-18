# 🔄 Main HIL Process (Level 1)

This is the highest-level view of the HIL loop. Click a block to open its detailed process.

```mermaid
flowchart TD
    classDef mainBox fill:#2b6cb0,stroke:#63b3ed,color:#fff,stroke-width:2px;
    classDef startEnd fill:#2d3748,stroke:#cbd5e0,color:#fff,stroke-width:1px;

    Start([Start HIL Loop]):::startEnd --> Build[1. Build ECU Image]:::mainBox
    Build --> Flash[2. Flash Target]:::mainBox
    Flash --> Test[3. Run HIL Tests]:::mainBox
    Test --> Analyze{Analyze Results}:::mainBox

    Analyze -->|Success / Pass| End([Complete / Release]):::startEnd
    Analyze -->|Error / Fail| Fix[4. Fix Code & Start Next Iteration]:::mainBox
    Fix --> Build

    %% Click a block to open its detailed process
    click Build "../04_fix_build_details/" "Open ECU image build details"
    click Flash "../02_flash_details/" "Open the target flashing process"
    click Test "../03_test_details/" "Open the HIL test execution process"
    click Analyze "../03_test_details/" "Open the results analysis process"
    click Fix "../04_fix_build_details/" "Open the code fix and rebuild process"
```

Open details in the VS Code Markdown preview: [Build](./04_fix_build_details.md) | [Flash](./02_flash_details.md) | [Tests and Results](./03_test_details.md) | [Code Fixes](./04_fix_build_details.md).