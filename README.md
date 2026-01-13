# Coral Reef Health Monitoring using CNN Image Classification

## Background
Coral reefs are among the most important marine ecosystems on Earth. They support high biodiversity and provide essential services such as coastal protection, tourism income, and fisheries. In recent years, coral bleaching has become more frequent due to rising sea temperatures and other environmental pressures. Monitoring reef health quickly and accurately is crucial to protect these ecosystems.

## Problem Statement
Bleaching detection is often performed manually by experts who inspect underwater imagery. This approach is accurate but slow and expensive, making it difficult to scale to large reef systems and frequent monitoring cycles.

## Proposed Approach
This project proposes a deep learning solution using a Convolutional Neural Network (CNN) to classify coral images into health-related categories (e.g., healthy vs. bleached). The model is trained on labelled reef imagery and evaluated using standard performance metrics to ensure reliability.

## Why CNN?
CNNs are effective for image-based tasks because they automatically learn visual features such as textures, shapes, and colour patterns. This makes them suitable for recognising bleaching cues in coral imagery.

## Key Benefits
1. **Efficiency:** Speeds up coral health assessment by automating classification.
2. **Scalability:** Supports analysis of large datasets and wide reef coverage.
3. **Consistency:** Produces stable predictions with reduced subjectivity.
4. **Faster response:** Enables earlier detection of bleaching events when paired with imaging systems.
5. **Decision support:** Helps researchers and policymakers prioritise conservation and restoration actions.
6. **Awareness:** Demonstrates how AI can support environmental sustainability efforts.

## Data Description (CSV)
The dataset includes annotation and label information that is used to generate training targets for the classification model.  
Update this section with your actual columns, for example:
- `Name`: image filename
- `Row`, `Column`: annotation coordinate
- `Label`: category at that coordinate
(If you aggregate per-image labels, mention the aggregation method: majority label, top-N classes, etc.)

## Output
The final model predicts coral health classes for new images and can be extended for monitoring workflows.
