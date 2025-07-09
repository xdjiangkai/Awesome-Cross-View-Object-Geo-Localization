# Awesome Cross-View Object Geo-Localization (CVOGL)

A curated list of state-of-the-art methods, datasets, and resources for **Cross-View Object Geo-Localization**, focusing on object-level alignment between ground/drone views and satellite imagery.

---

## Table of Contents
- [Methods](#methods)
- [Datasets](#datasets)
- [Key Challenges](#key-challenges)
- [Contributing](#contributing)

---

## Methods

### [2023 May] Cross-View Object Geo-Localization in a Local Region with Satellite Imagery [[Paper](https://ieeexplore.ieee.org/abstract/document/10226220)] [[Code](https://github.com/sunyuxi/DetGeo)]
- **Core Idea**: Addresses the limitations of traditional image-level localization by proposing a detection-based framework for object-level cross-view geo-localization, enabling precise localization of specific objects in satellite images using ground or drone query images  
- **Key Modules**:
  - **Two-Branch Encoder**: The query encoder (ResNet18) extracts features from ground/drone images with positional encoding of click points; the reference encoder (Darknet-53) processes satellite images
  - **Query-Aware Cross-View Fusion Module**: Employs cross-view spatial attention to dynamically adjust focus on satellite regions based on query features
  - **Loss Function**: Combines classification loss (binary cross-entropy) and localization loss (mean squared error) to jointly optimize matching and bounding box regression
- **Performance**: On the CVOGL dataset, achieves **45.43%** Acc@0.25 for *Ground → Satellite* and **61.97%** for *Drone → Satellite*, outperforming prior methods like SAFA by over 20%

---

### [2025 September] Improving Cross-view Object Geo-localization: A Dual Attention Approach with Cross-view Interaction and Multi-Scale Spatial Features [[Paper](https://openreview.net/pdf?id=LnRegTxsa4)] [Code]
- **Core Idea**: Address information transfer inefficiency and edge noise interference in cross-view localization by introducing dual attention mechanisms for enhanced feature interaction and multi-scale spatial perception.
- **Key Modules**:
  - **Cross-view and Cross-attention Module**: Conducts multiple iterations of cross-attention between query and reference features, enabling bidirectional contextual information exchange to suppress irrelevant noise. 
  - **Multi-head Spatial Attention Module**: Uses three attention heads with different convolutional kernel sizes (1×1, 3×3, 5×5) to extract multi-scale spatial features, enhancing local feature representation of target objects. 
- **Performance**: On CVOGL dataset, achieves 50.57% acc@0.25 for Ground→Satellite and 70.71% for Drone→Satellite tasks, outperforming DetGeo by 5.14% and 8.74% respectively; on G2D dataset, Ground→Drone task reaches 77.30% acc@0.25. 

---

### [2025 January] VAGeo: View-Specific Attention for Cross-View Object Geo-Localization [[Paper](https://arxiv.org/pdf/2501.07194)] [Code not available]
- **Core Idea**: Addresses inherent viewpoint discrepancies between ground/drone and satellite imagery by introducing view-specific positional encoding and hybrid attention
- **Key Modules**:
  - **View-Specific Positional Encoding**:  
    - *Ground view*: Uses a Laplacian distribution to emphasize the click-point region and suppress irrelevant background (e.g., sky, shadows)  
    - *Drone view*: Adopts adaptive ring-region partitioning with distance-decaying weights to capture spatial correlation with satellite images  
  - **Channel-Spatial Hybrid Attention**: Combines channel-wise and spatial attention to enhance feature discrimination
- **Performance**: On the CVOGL dataset, improves *Ground → Satellite* Acc@0.25 from **45.43%** to **48.21%**, and *Drone → Satellite* from **61.97%** to **66.19%**

---

### [2025 March] Attention-Driven Object Encoding and Multiscale Contextual Perception for Improved Cross-View Object Geo-Localization [[Paper](https://ieeexplore.ieee.org/abstract/document/10964230)] [[Code](https://github.com/HaoshuaiSong/AMPNet-CVOGL)]
- **Core Idea**: Enhances object shape/size modeling and handles scale variation in remote sensing images through multiscale feature extraction
- **Key Modules**:
  - **Attention-Driven Object Encoding**: Segments objects using SAM (Segment Anything Model) and integrates geometric priors (shape, size) into feature representation  
  - **Cross-View Multiscale Perception**: Applies parallel depth-wise convolutions (3×3, 5×5, 7×7) and MLP-based channel interactions to capture multiscale context
- **Performance**: Achieves *Drone → Satellite* Acc@0.25 of **73.28%** on CVOGL (↑11.31% over DetGeo)

---

### [2025 May] Object-Level Cross-View Geo-Localization with Location Enhancement and Multi-Head Cross Attention [[Paper](https://arxiv.org/pdf/2505.17911)] [[Code](https://github.com/ZheyangH/OCGNet)]
- **Core Idea**: Enhances spatial information retention and enables adaptive feature matching for visually similar objects across views
- **Key Modules**:
  - **Gaussian Kernel Transfer**: Replaces Euclidean distance encoding with a Gaussian kernel centered on the click point, suppressing distant noise  
  - **Location Enhancement (LE) Module**: Re-injects spatial cues during the final stage of matching to preserve object fidelity  
  - **Multi-Head Cross Attention**: Aligns query and reference features in a shared embedding space while attending to object-relevant regions
- **Performance**: On the CVOGL dataset, achieves *Drone → Satellite* Acc@0.25 of **68.35%**, with strong few-shot generalization (**29.17%** Acc@0.25 on novel classes)




---

## Datasets

| Dataset         | Views                   | Size                    | Annotations                        | Key Features                                                                 |
|------------------|--------------------------|---------------------------|------------------------------------|-------------------------------------------------------------------------------|
| **CVOGL**         | Ground / Drone + Satellite | 12,000 instances          | Click points, bounding boxes       | Objects include buildings, bridges, roundabouts; large-scale variation (500–18,000 m²) |
| **CVOGL-FewShot** | Drone + Satellite         | 52 instances (4 new classes) | Click points, bounding boxes       | Extends CVOGL with novel object types (e.g., lake, port) for few-shot evaluation        |

---

## Key Challenges

1. **Viewpoint Discrepancy**  
   Large perspective gaps between ground/drone and satellite views cause severe domain shifts and visual ambiguity

2. **Scale Variation**  
   Object sizes vary drastically (500–18,000 m²), complicating consistent feature learning across views

3. **Semantic Inconsistency**  
   Features extracted from different viewpoints often misalign, especially in dual-branch architectures

4. **Few-Shot Generalization**  
   Annotated samples for rare object types (e.g., ports, lakes) are scarce, making generalization difficult

---

## Contributing

Additions of new methods, datasets, or open-source implementations are welcome! Please open a pull request with:

- Method or dataset name and a concise description
- Relevant paper citation and performance metrics
- Link to open-source code (if available)

---

*If you find this list useful, consider starring the repository and citing relevant papers.*
