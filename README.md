# Awesome Cross-View Object Geo-Localization (CVOGL)

A curated list of state-of-the-art methods, datasets, and resources for **Cross-View Object Geo-Localization**, focusing on object-level alignment between ground/drone views and satellite imagery.


## Table of Contents
- [Methods](#methods)
  - [View-Specific Attention Methods](#view-specific-attention-methods)
  - [Semantic Consistency & Feature Fusion Methods](#semantic-consistency--feature-fusion-methods)
  - [Multiscale Perception Methods](#multiscale-perception-methods)
  - [Location Enhancement Methods](#location-enhancement-methods)
- [Datasets](#datasets)
- [Open-Source Codes](#open-source-codes)
- [Key Challenges](#key-challenges)


## Methods

### View-Specific Attention Methods
#### VAGeo: View-specific Attention for CVOGL
- **Core Idea**: Address inherent viewpoint discrepancies between ground/drone views and satellite imagery by designing view-specific positional encoding and hybrid attention.
- **Key Modules**:
  - **View-Specific Positional Encoding (VSPE)**: 
    - Ground view: Uses Laplacian distribution to focus on click-point regions and suppress background (e.g., sky, shadows) .
    - Drone view: Adopts adaptive ring-region partitioning with distance-decaying weights, leveraging spatial correlation with satellite views .
  - **Channel-Spatial Hybrid Attention (CSHA)**: Combines channel attention (refines feature dimensions) and spatial attention (enhances local details) to learn discriminative features .
- **Performance**: On CVOGL dataset, improves ground→satellite acc@0.25 from 45.43% to 48.21%, and drone→satellite from 61.97% to 66.19% .


### Semantic Consistency & Feature Fusion Methods
#### Dual-Branch Network with FCE and MLFM
- **Core Idea**: Enhance semantic representation in multi-view geo-localization by improving feature consistency across branches and fusing multi-level features.
- **Key Modules**:
  - **Feature Consistency Enhancement (FCE)**: Uses channel and spatial attention to align salient region features between dual branches, ensuring semantic consistency .
  - **Multi-Level Feature Mining (MLFM)**: Integrates low-level details (edges, textures) and high-level semantics (global layout) to capture comprehensive information .
- **Performance**: Achieves 82.38% AP for drone→satellite and 77.36% AP for satellite→drone matching on University-1652 dataset .


### Multiscale Perception Methods
#### AMPNet: Attention-Driven Multiscale Perception Network
- **Core Idea**: Improve object shape/size modeling and handle scale variations in remote sensing images.
- **Key Modules**:
  - **Attention-Driven Object Encoding (ADOE)**: Uses SAM (Segment Anything Model) to segment objects, integrating geometric priors (shape/size) into feature learning .
  - **Cross-View Multiscale Perception (CVMSP)**: Captures multiscale context via parallel depth-wise convolutions (3×3, 5×5, 7×7) and enhances channel interactions with MLP .
- **Performance**: On CVOGL dataset, drone→satellite acc@0.25 reaches 73.28% (11.31% improvement over DetGeo) .


### Location Enhancement Methods
#### OCGNet: Object-level Cross-view Geo-localization Network
- **Core Idea**: Enhance location information retention and adaptive feature matching for visually similar objects.
- **Key Modules**:
  - **Gaussian Kernel Transfer (GKT)**: Replaces Euclidean distance encoding with Gaussian kernel to focus attention on click-point regions, reducing noise from distant areas .
  - **Location Enhancement (LE) Module**: Reinjects location cues in late-stage feature matching to preserve spatial fidelity .
  - **Multi-Head Cross Attention (MHCA)**: Aligns query and reference features in a shared space, adaptively emphasizing object-specific regions .
- **Performance**: On CVOGL dataset, drone→satellite acc@0.25 reaches 68.35%, with strong few-shot generalization (29.17% acc@0.25 on novel classes) .


## Datasets
| Dataset       | Views                  | Size                | Annotations                          | Key Features                                  |
|---------------|------------------------|---------------------|--------------------------------------|-----------------------------------------------|
| CVOGL         | Ground/drone + Satellite | 12k instances       | Click points, bounding boxes         | Objects: buildings, bridges, roundabouts; large scale variations (500–18,000 m²) .
| University-1652 | Ground/drone + Satellite | 1652 geographic targets | Multi-view images per target        | Covers 72 universities; supports multi-source view matching .
| CVOGL-fewshot | Drone + Satellite      | 52 instances (4 new classes) | Click points, bounding boxes         | Extends CVOGL with novel objects (lake, port) for few-shot evaluation .


## Open-Source Codes
- **AMPNet**: [GitHub](https://github.com/HaoshuaiSong/AMPNet-CVOGL) .
- **OCGNet**: [GitHub](https://github.com/ZheyangH/OCGNet) .
- **DetGeo**: [GitHub](https://github.com/sunyuxi/DetGeo) .


## Key Challenges
1. **Viewpoint Discrepancies**: Large differences in perspective (e.g., ground vs. satellite) lead to visual ambiguity .
2. **Scale Variations**: Objects in satellite images vary drastically in size (500–18,000 m²), challenging consistent feature learning .
3. **Semantic Consistency**: Dual-branch networks often learn inconsistent features for salient regions across views .
4. **Few-Shot Generalization**: Limited annotated data for rare object classes (e.g., ports, lakes) .


## Contributing
Additions of new methods, datasets, or codes are welcome! Please open a PR with:
- Method/dataset name and key details.
- Relevant paper citation and performance metrics.
- Link to open-source resources (if available).
