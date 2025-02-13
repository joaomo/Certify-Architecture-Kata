# ADR: Intelligent Case Study Generation

## ADR ID: 004  

## Date: 2023-10-XX  

## Status: Proposed

---

## 1. Introduction

Intelligent Case Study Generation for SoftArchCert Using AI

---

## 2. Context and Problem Statement

**Background:**  
Certifiable, Inc.'s SoftArchCert system currently uses a fixed set of case studies for the architecture submission test (Test 2). These case studies are manually created and periodically revised by expert software architects. With the expansion of the certification program (anticipating a 5–10× increase in submissions) and the rapid evolution of industry practices, maintaining an up-to-date, diverse, and challenging portfolio of case studies has become increasingly difficult.

**Problem:**  

- **Manual Effort:** Creating and updating case studies manually is resource-intensive and slow.  
- **Content Staleness:** Pre-existing case studies risk becoming outdated as architectural practices and technologies evolve.  
- **Security Concerns:** Fixed case studies may leak over time, reducing the exam's effectiveness and compromising the certification's integrity.
- **Scalability:** Increasing candidate volume requires a larger and more varied set of case studies to ensure fairness and maintain exam integrity.

---

## 3. Possible Solutions

1. **Maintain Full Manual Case Study Creation:**  
   - **Pros:** Ensures high domain quality and human creativity.  
   - **Cons:** Does not scale with rapid candidate growth; susceptible to content staleness and increased workload on experts.

2. **Fully Automated Generation Without Review:**  
   - **Pros:** Maximum scalability and minimal human intervention.  
   - **Cons:** Risk of generating case studies that are off-target, lack nuance, or may not align well with certification standards.

3. **Hybrid Intelligent Generation with Human Oversight (Chosen Option):**  
   - **Pros:** Balances automation with quality control; AI generates diverse and timely case studies while experts review and fine-tune the outputs, ensuring security and relevance.  
   - **Cons:** Increased system complexity and the need for an integrated review interface add to the overhead.

4. **Template-Based Rule-Driven Generation:**  
   - **Pros:** Deterministic and transparent outcomes.  
   - **Cons:** Inflexible and unable to capture the creative and adaptive aspects of modern architectural challenges.

---

## 4. Trade-Off Analysis

1. **Automation vs. Human Oversight:**
   - **Pros:** Automation scales well and reduces manual effort.
   - **Cons:** Requires robust human oversight to ensure quality and relevance.

2. **Complexity vs. Maintainability:**
   - **Pros:** A sophisticated system can handle diverse and dynamic content.
   - **Cons:** Increased complexity requires ongoing maintenance and monitoring.

3. **Scalability vs. Quality Assurance:**
   - **Pros:** Automated generation scales effortlessly.
   - **Cons:** Ensuring high-quality output necessitates rigorous review processes.

4. **Flexibility vs. Determinism:**
   - **Pros:** AI-generated content is flexible and adaptive.
   - **Cons:** Requires careful prompt engineering and validation to avoid inconsistencies.

---

## 5. Proposed Solution

**Chosen Approach:**  
Implement an Intelligent Case Study Generation module that:

- Uses a fine-tuned Large Language Model (LLM) and prompt engineering to generate realistic, varied, and industry-relevant case studies.
- Dynamically generates new case studies on demand or on a scheduled basis, incorporating the latest architectural trends and best practices.
- Provides different levels of complexity tailored to candidate experience or exam difficulty.
- Includes mechanisms for human review and feedback to ensure the generated case studies meet quality and security standards.
- Integrates with the SoftArchCert system's administrative interfaces, allowing designated experts to approve, modify, or retire generated case studies.

### Components

1. **Large Language Model (LLM):**
   - **Technology:** OpenAI GPT-4 or similar
   - **Purpose:** Generate diverse and realistic case studies based on prompt engineering.
   - **Implementation Strategy:** Fine-tune the LLM using historical case studies and industry data to ensure relevance and accuracy.

2. **Prompt Engineering Module:**
   - **Technology:** Custom Python scripts
   - **Purpose:** Craft prompts that guide the LLM to produce high-quality case studies.
   - **Implementation Strategy:** Develop a library of prompts that cover various architectural scenarios and complexities.

#### Prompt Engineering Approaches

1. **One-Shot Learning:**
   - **Description:** Provide a single example in the prompt to guide the LLM in generating the desired output.
   - **Pros:** Simple to implement and requires minimal data preparation.
   - **Cons:** May not be sufficient for complex or nuanced case studies, leading to less accurate or relevant outputs.
   - **Use Case:** Suitable for generating straightforward case studies with well-defined structures.

2. **Few-Shot Learning:**
   - **Description:** Provide a few examples (typically 2-5) in the prompt to help the LLM understand the desired format and content.
   - **Pros:** Balances simplicity and effectiveness, improving the quality and relevance of generated case studies.
   - **Cons:** Requires more data preparation than one-shot learning but still manageable.
   - **Use Case:** Ideal for generating more complex case studies that require a deeper understanding of context and structure.

3. **Zero-Shot Learning:**
   - **Description:** Provide a detailed prompt without examples, relying on the LLM's pre-trained knowledge to generate the output.
   - **Pros:** No need for example data, leveraging the LLM's extensive training.
   - **Cons:** May result in less accurate or relevant outputs, especially for highly specific or complex scenarios.
   - **Use Case:** Useful for exploratory generation or when example data is unavailable.

4. **Multi-Turn Prompting:**
   - **Description:** Engage the LLM in a multi-turn dialogue, refining the prompt and responses iteratively to achieve the desired output.
   - **Pros:** Allows for iterative refinement, improving the quality and relevance of the generated content.
   - **Cons:** More complex to implement and may require additional computational resources.
   - **Use Case:** Suitable for generating highly detailed and nuanced case studies where initial prompts may need refinement.

5. **Contextual Prompting:**
   - **Description:** Provide additional context or background information along with the prompt to guide the LLM in generating the output.
   - **Pros:** Enhances the relevance and accuracy of the generated content by providing more context.
   - **Cons:** Requires careful crafting of context information to avoid overwhelming the LLM.
   - **Use Case:** Ideal for generating case studies that require a deep understanding of specific contexts or scenarios.

### Implementation Strategy

1. **Prototype Development:**
   - Develop a prototype using a fine-tuned LLM and prompt engineering.
   - Validate the prototype with a small set of historical case studies.

2. **Human Review Interface:**
   - Design and implement the review interface with features for expert feedback and approval.
   - Ensure the interface is intuitive and integrates seamlessly with the generation module.

3. **Integration Testing:**
   - Conduct thorough testing to ensure all components work together as expected.
   - Validate data flow and security between the generation module, review interface, and SoftArchCert system.

4. **Pilot Program:**
   - Run a pilot program to gather feedback from experts and candidates.
   - Use the feedback to refine the generation process and review interface.

5. **Full Scale Rollout:**
   - Gradually transition to using AI-generated case studies.
   - Implement continuous monitoring, logging, and periodic re-training of the LLM.

---

## 6. Resulting Architecture

### Overview

The architecture for the Intelligent Case Study Generation module will leverage a combination of AI technologies, cloud infrastructure, and human-in-the-loop processes to ensure scalability, relevance, and quality. The solution will be designed to integrate seamlessly with the existing SoftArchCert system.

### Architecture Diagram

```mermaid
graph LR
    subgraph SoftArchCert System
        subgraph Candidate Subsystem
            CAUI[Candidate User Interface]
            CD[Candidate Database]
        end

        subgraph Expert Subsystem
            EGUI[Expert Grading User Interface]
            EPD[Expert Profile Database]
        end

        subgraph Aptitude Testing Subsystem
            ATUI[Aptitude Test User Interface]
            ATD[Aptitude Test Database]
            ATUD[Aptitude Test Ungraded Database]
            ATG[Aptitude Test Grading Service]
        end

        subgraph Architecture Submission Subsystem
            CSD[Case Study Database]
            ASU[Architecture Submission Upload]
            AGF[Architecture Grade & Feedback Database]
        end

        subgraph Certification Management
            CMD[Candidate Status Database]
            CDV[Certification Database]
            CSG[Certification Generation Service]
        end

        subgraph Admin Subsystem
            AUI[Admin User Interface]
        end

        subgraph Intelligent Case Study Generation
            LLM[Large Language Model]
            PEM[Prompt Engineering Module]
            HRI[Human Review Interface]
            IS[Integration Services]
            DS[Data Storage]
        end
    end
    
    CAUI --> CD
    
    EGUI --> EPD
    EGUI --> AGF

    ATUI --> ATD
    ATUI --> ATUD
    ATUI --> ATG
    ATG --> ATUD

    ASU --> CSD
    ASU --> AGF
    
    CMD --> CDV
    CMD --> AGF
    CSG --> CDV

    AUI --> EPD
    AUI --> ATD
    AUI --> CSD

    LLM --> PEM
    PEM --> HRI
    HRI --> IS
    IS --> DS
    IS --> CSD

    style SoftArchCert System fill:#f9f,stroke:#333,stroke-width:2px
    style Intelligent Case Study Generation fill:#bbf,stroke:#333,stroke-width:2px