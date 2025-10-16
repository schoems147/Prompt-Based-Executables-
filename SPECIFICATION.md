# Prompt-Based Executable (PBE) Specification v1.0

## Overview

A Prompt-Based Executable (PBE) is a JSON file containing structured instructions that configure LLM behavior. PBEs enable reproducible, portable AI interactions across different systems.

---

## File Format

- **Extension**: `.pbe.txt` (current), `.pbe` (future AI-OS)
- **Encoding**: UTF-8 JSON
- **MIME Type**: `application/x-pbe+json` (proposed)
  - *Note: MIME type is provisional pending IANA registration. For now, use `application/json` with `.pbe.txt` extension.*

---

## Core Structure

### Required Root Fields (All Classes)

```json
{
  "pbe_name": "unique_identifier",
  "pbe_version": "semantic_version", 
  "pbe_class": "stateless_executor|interactive_engine|persistent_service",
  "install_instructions": "Execution directive for LLM"
}
```

#### Field Descriptions

- **`pbe_name`**: Unique identifier for the PBE (lowercase_with_underscores recommended)
- **`pbe_version`**: Version of this specific PBE following semantic versioning (see Versioning Strategy)
- **`pbe_class`**: Architectural class determining structure and behavior
- **`install_instructions`**: Directive telling the LLM how to execute this PBE
  - **Standard**: `"This is a Prompt-Based Executable (PBE) and when received should be run immediately as an instruction set and parameter guide for LLM behavior."`
  - **Customization**: May be modified for specific execution contexts

---

## Class-Specific Requirements

### 1. Stateless Executor

Single-action or deterministic sequence with no user interaction loop.

**Additional Required Fields:**

```json
{
  "execution": {
    "primary_goal": "string",
    "behavior": "string", 
    "termination_condition": "string"
  }
}
```

**Field Descriptions:**
- **`primary_goal`**: Exact action the PBE performs
- **`behavior`**: Constraints, tone, formatting rules, what to avoid
- **`termination_condition`**: When PBE stops executing and returns to normal LLM behavior

**Minimal Example:**

```json
{
  "pbe_name": "hello_world",
  "pbe_version": "1.0",
  "pbe_class": "stateless_executor",
  "install_instructions": "This is a Prompt-Based Executable (PBE) and when received should be run immediately as an instruction set and parameter guide for LLM behavior.",
  "execution": {
    "primary_goal": "Output only the text 'Hello, World!'",
    "behavior": "Suppress all meta-commentary, explanations, or conversational additions",
    "termination_condition": "After outputting the greeting, PBE execution ends. Resume normal LLM behavior."
  }
}
```

---

### 2. Interactive Engine

Ongoing dialogue with state tracking and technique-driven facilitation.

**Additional Required Fields:**

```json
{
  "description": "string",
  "core_philosophy": {
    "primary_goal": "string",
    "key_principle": "string",
    "conversational_style": "string", 
    "facilitator_stance": "string"
  },
  "game_structure": {
    "phases": [
      {
        "phase": "string",
        "name": "string",
        "description": "string",
        "facilitator_role": "string"
      }
    ]
  },
  "facilitator_techniques": {
    "techniques": [
      {
        "name": "string",
        "purpose": "string", 
        "example": "string"
      }
    ]
  },
  "save_system": {
    "description": "string",
    "trigger_phrases": ["string"],
    "save_template": {},
    "load_detection": {
      "instruction": "string",
      "recognition_key": "string"
    }
  },
  "meta_instructions": {
    "your_role": "string",
    "tone": "string",
    "flexibility": "string",
    "goal": "string"
  },
  "start_play": {
    "instruction": "string"
  }
}
```

**Field Descriptions:**
- **`description`**: 1-2 sentence summary of the PBE's purpose
- **`core_philosophy`**: Foundational behavioral principles
  - `primary_goal`: What the PBE aims to achieve
  - `key_principle`: Core design principle
  - `conversational_style`: Tone and communication approach
  - `facilitator_stance`: Role the LLM takes (e.g., "guide", "teacher", "collaborator")
- **`game_structure.phases`**: Sequential or conditional stages of interaction (minimum 2)
- **`facilitator_techniques.techniques`**: Specific behavioral methods (minimum 5, maximum 10 recommended)
  - Each must include: `name`, `purpose`, and concrete `example`
- **`save_system`**: State preservation mechanism
  - `trigger_phrases`: User commands to generate save file
  - `save_template`: JSON structure using `{pbe_name}_save` as root key
  - `load_detection`: Instructions for recognizing and resuming from save data
- **`meta_instructions`**: High-level behavioral guidance for the LLM
- **`start_play.instruction`**: Initial greeting/message when PBE loads

**Minimal Example:**

```json
{
  "pbe_name": "simple_quiz",
  "pbe_version": "1.0",
  "pbe_class": "interactive_engine",
  "install_instructions": "This is a Prompt-Based Executable (PBE) and when received should be run immediately as an instruction set and parameter guide for LLM behavior.",
  "description": "Interactive quiz that asks questions and tracks correct answers.",
  "core_philosophy": {
    "primary_goal": "Test user knowledge through questions",
    "key_principle": "Provide immediate feedback",
    "conversational_style": "Friendly and encouraging",
    "facilitator_stance": "Quiz master and educator"
  },
  "game_structure": {
    "phases": [
      {
        "phase": "1_question",
        "name": "Ask Question",
        "description": "Present question to user",
        "facilitator_role": "Ask clear questions, wait for response"
      },
      {
        "phase": "2_feedback",
        "name": "Provide Feedback",
        "description": "Evaluate answer and explain",
        "facilitator_role": "Confirm correctness, explain why"
      }
    ]
  },
  "facilitator_techniques": {
    "techniques": [
      {
        "name": "Clear Questioning",
        "purpose": "Ask unambiguous questions",
        "example": "What is the capital of France? A) London B) Paris C) Berlin"
      },
      {
        "name": "Positive Reinforcement",
        "purpose": "Encourage continued participation",
        "example": "Correct! Great job recognizing that."
      },
      {
        "name": "Constructive Correction",
        "purpose": "Gently correct wrong answers",
        "example": "Not quite—the correct answer is B. Here's why..."
      },
      {
        "name": "Progress Tracking",
        "purpose": "Show user their score",
        "example": "You've answered 7 out of 10 correctly so far!"
      },
      {
        "name": "Adaptive Difficulty",
        "purpose": "Adjust question complexity",
        "example": "You're doing great—let's try a harder one."
      }
    ]
  },
  "save_system": {
    "description": "Save quiz progress including score and question history",
    "trigger_phrases": ["save my progress", "save quiz"],
    "save_template": {
      "simple_quiz_save": {
        "pbe_version": "1.0",
        "save_date": "YYYY-MM-DD",
        "score": 0,
        "total_questions": 0,
        "question_history": []
      }
    },
    "load_detection": {
      "instruction": "When you receive JSON with root key 'simple_quiz_save', acknowledge the save, display current score, and ask if user wants to continue.",
      "recognition_key": "simple_quiz_save"
    }
  },
  "meta_instructions": {
    "your_role": "Educational quiz facilitator",
    "tone": "Encouraging and informative",
    "flexibility": "Adapt question difficulty to user performance",
    "goal": "Help user learn while tracking their progress"
  },
  "start_play": {
    "instruction": "Welcome to the quiz! I'll ask you questions and track your score. Ready for the first question?"
  }
}
```

---

### 3. Persistent Service

Background monitors or continuous processes (future AI-OS feature).

**Additional Required Fields:**

```json
{
  "service_config": {
    "monitoring_target": "string",
    "activation_conditions": "string",
    "background_operation": "string"
  }
}
```

**Status**: Specification incomplete—reserved for AI-OS development.

---

## Execution Semantics

### Loading

When an LLM receives a PBE:

1. Parse JSON and validate required fields for the specified `pbe_class`
2. Set behavioral parameters according to class-specific structure
3. Execute `start_play.instruction` (if present)
4. Enter defined interaction pattern

### State Management

- **Interactive Engines**: Must maintain conversation state across messages
- **Save Systems**: Use `{pbe_name}_save` root key for portability and consistency
- **Load Detection**: Auto-resume when save data with matching recognition key is detected

### Termination

- **Stateless Executor**: After `termination_condition` is met, return to normal LLM behavior
- **Interactive Engine**: Continue until explicit user exit command or defined completion state
- **Persistent Service**: Continuous operation until system-level intervention

---

## Validation Rules

1. **`pbe_name`**: Must use `lowercase_with_underscores`, must be unique identifier
2. **`pbe_version`**: Must follow semantic versioning (MAJOR.MINOR.PATCH)
3. **`facilitator_techniques`**: Interactive engines require 5-10 techniques, each with `name`, `purpose`, and `example`
4. **`save_template`**: Must use `{pbe_name}_save` as root key pattern
5. **`game_structure.phases`**: Interactive engines require minimum 2 phases
6. **JSON Structure**: Must be valid, parseable JSON with proper encoding

---

## Versioning Strategy

PBE versions follow **semantic versioning** (SemVer):

```
MAJOR.MINOR.PATCH

Examples: 1.0.0, 1.2.0, 2.0.0
```

**Version Increment Guidelines:**

- **MAJOR**: Breaking changes to PBE behavior or structure incompatible with previous versions
  - Example: Changing required fields, restructuring save format
- **MINOR**: New features or enhancements, backward-compatible
  - Example: Adding new techniques, optional fields, or phases
- **PATCH**: Bug fixes, clarifications, or minor improvements
  - Example: Fixing typos, clarifying instructions, improving examples

**Note**: The `pbe_version` field refers to the version of the individual PBE, not the specification version.

---

## Reserved Field Names

The following fields are reserved across all PBE classes and should not be overridden or used for custom purposes:

### Universal Reserved Fields
- `pbe_name`
- `pbe_version`
- `pbe_class`
- `install_instructions`

### Class-Specific Reserved Fields

**Stateless Executor:**
- `execution`

**Interactive Engine:**
- `description`
- `core_philosophy`
- `game_structure`
- `facilitator_techniques`
- `save_system`
- `meta_instructions`
- `start_play`

**Persistent Service:**
- `service_config`

Custom fields may be added outside these reserved names for extended functionality.

---

## Interoperability

PBEs are designed to work across LLM platforms with varying degrees of fidelity.

### Tested Platforms
- **Claude** (Anthropic)
- **ChatGPT** (OpenAI)
- **Gemini** (Google)
- **Grok** (xAI)
- **DeepSeek** (DeepSeek AI)

### Compatibility Requirements
- LLM must support JSON parsing
- LLM must follow structured instructions
- LLM must maintain conversation context (for interactive engines)

### Platform-Specific Notes
- **Execution Fidelity**: Behavior depends on LLM's instruction-following capability
- **Field Support**: Some platforms may ignore or interpret certain fields differently
- **Save/Load Features**: Require conversation persistence and file handling capabilities
- **No Guarantees**: Identical behavior across platforms is not guaranteed but is the design goal

### Best Practices for Portability
- Test PBEs on multiple platforms before distribution
- Use clear, explicit instructions in all fields
- Avoid platform-specific features or terminology
- Document any known platform limitations

---

## Security Considerations

### Transparency
- PBEs are human-readable JSON for full transparency
- Users should audit unfamiliar PBEs before execution
- All behavioral instructions are explicit in the file structure

### Permissions
- PBEs have no implicit system access or elevated permissions
- Execution is constrained to LLM conversational capabilities
- Cannot access files, networks, or system resources beyond LLM's standard functionality

### Trust Model
- PBEs from unknown sources should be treated as untrusted code
- Recommend community review and verification for shared PBEs
- Version control and cryptographic signing (future consideration)

### Malicious Use Prevention
- PBEs cannot execute arbitrary code outside LLM context
- Cannot modify system state or access sensitive data
- Behavioral scope limited to text generation and conversation

---

## Contributing PBEs

To submit a PBE to the ecosystem:

### Submission Requirements

1. **Validate**: Ensure full compliance with this specification
2. **Test**: Run on at least 2 different LLM platforms and document results
3. **Document**: Include clear description, use case, and example output
4. **License**: Specify open-source license (MIT recommended)
5. **Submit**: Pull request to `/pbes/[appropriate_class]/`

### Quality Standards

- **Interactive Engines**: Must include 5+ techniques with concrete examples
- **Save Systems**: Required if state preservation is relevant to functionality
- **Termination Conditions**: Must be clearly defined for stateless executors
- **Examples**: Provide at least one example interaction or output
- **Clarity**: All instructions must be unambiguous and actionable

### Contribution Process

1. Fork the repository
2. Add your PBE to the appropriate class folder
3. Update any relevant documentation
4. Submit pull request with description of PBE functionality
5. Respond to reviewer feedback

---

## Changelog

### v1.0 (2025-10-16)
- Initial specification release
- Three classes defined: `stateless_executor`, `interactive_engine`, `persistent_service`
- Save system standardization with `{pbe_name}_save` pattern
- Validation rules established
- Semantic versioning guidelines
- Reserved field names documented
- Interoperability guidelines
- Security considerations
- Contribution guidelines
- Tested on Claude, ChatGPT, Gemini, Grok, and DeepSeek

---

## Future Considerations

### Planned Features
- **Composability**: PBEs calling other PBEs
- **Persistent Service Class**: Full specification for background processes
- **Schema Validation**: Automated JSON schema validator tool
- **Registry System**: Centralized PBE discovery and distribution
- **Cryptographic Signing**: Verification of PBE authenticity

### Community Feedback
This specification is open to community input. Proposed changes should be submitted via GitHub issues with rationale and use cases.

---

## Reference Implementation

The **PBE Creator Tool (PBCT)** is the reference implementation for generating compliant PBEs through guided dialogue. See `/tools/pbct.txt` in the repository.

---

**Specification Maintainer**: Henko Schoeman  
**Last Updated**: 2025-10-16  
**License**: MIT License