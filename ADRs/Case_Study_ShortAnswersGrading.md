# ADR - Case Study Short Answer Grading

## ADR ID: 001

## Date: 2025-02-16

## Status: Proposed


## Context

Certifiable, Inc. anticipates a 5-10X increase in test submissions due to expanding enrollment and new partnerships. Test 1 comprises multiple-choice questions, which are automatically graded, and short-answer questions, which require manual grading by expert software architects. This manual process is time-consuming, taking up to three hours per candidate, and poses a risk to the company's one-week grading guarantee if enhancements are not implemented. Maintaining trust in grading integrity is crucial, as even minor misclassifications could damage the brand's reputation. The company faces scalability constraints, as hiring additional expert graders is both costly and slow, and a fully automated approach without oversight might undermine trust. Any new grading solution must integrate smoothly with existing test systems and data pipelines.

## Problem Statement

The challenge for Certifiable, Inc. is to introduce AI-driven short-answer grading to handle increased volumes without compromising accuracy and reputation. The solution must be scalable to manage the anticipated surge in submissions while maintaining or exceeding current human accuracy standards, with minimal false positives or negatives. Speed and efficiency are crucial for both candidate satisfaction and operational effectiveness. Retaining human oversight for ambiguous cases is essential to ensure the highest quality of results. Additionally, the system must integrate seamlessly with existing test interfaces and internal data repositories.

## Decision

Certifiable, Inc. will implement a hybrid AI-assisted grading system for Test 1. Semantic similarity models will be used to evaluate short-answer responses by comparing them to ideal answers, combined with multiple-choice scores to propose pass/fail decisions to experts. Retrieval-Augmented Generation (RAG) will provide feedback and highlight areas needing human input, ensuring targeted expert review.

### Justification

**Efficiency and Scalability:**
Semantic similarity models are computationally efficient, allowing for rapid processing of large volumes of data. This makes them well-suited for handling the anticipated surge in test submissions without compromising speed.

**Cost-Effectiveness:**
By avoiding the need for extensive fine-tuning of large language models or NLP classifiers, this approach reduces both the financial and data requirements, making it a more feasible option given current resources.

**Enhanced Feedback and Focused Human Oversight:**
RAG provides detailed, contextually relevant feedback that can be reviewed by experts, ensuring candidates receive clear guidance on their performance. Additionally, RAG highlights specific areas needing human input, allowing experts to concentrate their efforts where they are most needed.

**Maintaining Quality and Integrity:**
By combining AI-driven evaluations with human oversight for ambiguous cases, the system maintains high grading standards and minimizes the risk of false positives, preserving the certification's credibility.

### Trade-off Analysis

**Accuracy vs. Cost:**
While fine-tuning LLMs or NLP classifiers could potentially offer higher accuracy, the associated costs and data requirements make semantic similarity models a more practical choice. This approach balances the need for accuracy with budgetary constraints.

**Speed vs. Human Involvement:**
The use of AI models accelerates the grading process, but human oversight is still necessary for ambiguous cases. This trade-off ensures that while grading is faster, quality is not compromised.

**Feedback Quality vs. Implementation Complexity:**
Implementing RAG adds complexity to the system but significantly enhances the quality of feedback provided to candidates. This trade-off is justified by the improved candidate experience and the fairness when providing feedback across candidates, ensuring consistent and equitable evaluations.

### Assumptions

**Quality of Training Data:**
It is assumed that the historical data used to train the semantic similarity models is of high quality, comprehensive, and representative of the types of responses candidates will provide. This includes having a well-defined set of ideal answers for comparison.

**Model Performance:**
We assume that the semantic similarity models will accurately assess the quality of short-answer responses based on their similarity to ideal answers. This includes the expectation that the models can effectively handle variations in phrasing and terminology used by candidates.

**Human Oversight Effectiveness:**
We assume that human experts will be able to effectively review and validate the AI-generated scores, especially for borderline cases. This includes the expectation that experts can provide valuable feedback to improve the AI models over time.

**Feedback Utility:**
It is assumed that the feedback generated by RAG will be relevant, actionable, and clear enough for candidates to understand their performance and areas for improvement.

**Integration Capability:**
It is assumed that the AI solutions can be seamlessly integrated with existing test delivery and grading systems without significant technical challenges or disruptions to current workflows.

**Data:**
We assume the data from the completed tests includes annotations indicating pass/fail status and links to the feedback provided to candidates for each short-answer question.

## Implementation Plan

### Phase 1: Feedback Generation Setup

During this phase, the RAG system will be configured to generate pre-written feedback based on candidate responses, utilizing a library of feedback developed for both approval and failure cases. The system will provide experts with options for feedback, allowing them to select the most appropriate response to send to candidates. This setup will significantly reduce the time experts spend crafting individual feedback, streamlining the review process. Rigorous testing will be conducted to ensure that the generated feedback is relevant, clear, and actionable.

### Phase 2: Integration of Semantic Analysis and Feedback Loop

In this phase, the semantic similarity analysis will be fully integrated into the grading system. The analysis will evaluate candidate responses against the predefined set of top-selected answers, providing automated grading suggestions along with confidence intervals for each response. Experts will receive these suggestions alongside the pre-written feedback generated in the previous phase, allowing them to make informed decisions on whether to agree with or override the AI's grading suggestions. A feedback loop will be established, where experts can provide input on the AI's performance, particularly in cases where the confidence interval is low or where the AI's suggestions are disputed. This feedback will be used to continuously refine the semantic analysis model and improve its accuracy over time. Additionally, when the semantic analysis fails to provide a clear grading decision, the system will retrieve relevant examples from the RAG knowledge base to assist experts in making informed decisions. This approach ensures that the grading process remains efficient while maintaining high standards of accuracy and quality

### Phase 3: Automated Grading with Quality Control

In this phase, the system will leverage the results from the semantic similarity analysis alongside the multiple-choice scores to identify cases where there is strong evidence indicating that a candidate passes. For these cases, the system will automate the grading process, allowing candidates to move on to the second test without human intervention. To maintain quality control, a small sample of these automated decisions will be sent to human experts for review, ensuring that the system's accuracy is upheld. Additionally, for borderline cases where the confidence in the semantic analysis is lower or where there is potential for false negatives, human graders will be involved to assess the responses. If the human score is high in these borderline cases, candidates will also be allowed to progress to the second test. This approach balances efficiency with the need for oversight, ensuring that high-quality standards are maintained throughout the grading process.


## Resulting Architecure

The resulting architecture for Test 1 grading combines AI-driven semantic analysis with human oversight to enhance efficiency and maintain accuracy. Semantic similarity models analyze short-answer responses, comparing them to ideal answers and generating scores with confidence intervals. These scores are combined with multiple-choice results to create an overall confidence level for pass/fail decisions. High-confidence pass cases are automated, allowing candidates to proceed to Test 2 directly, with a small sample undergoing human quality control. Borderline cases and those with lower confidence are flagged for expert review. To aid experts, a Retrieval-Augmented Generation (RAG) system provides pre-written feedback options and relevant examples, particularly for ambiguous responses. A feedback loop is implemented, allowing expert graders to refine the semantic analysis model continuously. This hybrid approach optimizes grading speed, reduces expert workload, and ensures consistent, high-quality certification outcomes.

## References

1.  Sultan, A., & Salem, A. M. (2022). [Automated short answer grading systems: A systematic literature review](https://link.springer.com/article/10.1007/s10462-021-10068-2). *Education and Information Technologies*, *27*(7), 9485-9519.
2.  Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., ... & Kiela, D. (2020). [*Retrieval-augmented generation for knowledge-intensive NLP tasks*](https://proceedings.neurips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html). *arXiv preprint arXiv:2005.11401*.
3.  "Human-in-the-Loop Machine Learning." [*Google AI Blog*](https://ai.googleblog.com/2018/09/human-in-loop-machine-learning.html).