# SigspatialDemo

A demonstration of multimodal classification using CLIP embeddings, spatial grid references, and fusion strategies.

## 🔍 Tags (49)
We predict 49 multi-hot tags for each image. See `tags-top.csv` for the full list of human-readable tag names.

## 📚 Modalities
- **Image**: 256×256 geograph imagery.  
- **Text**: image `title` (caption).  
- **Location**: OS grid reference → projected into UK coordinates (2D normalized lat/lon or 3D sphere).  
- **Excluded**: satellite imagery, street-view, user IDs, or real names.

## 🔗 Fusion Strategies
Two primary fusion methods:

1. **Concatenation + MLP**  
   - Stack embeddings: `[image_emb ⊕ text_emb ⊕ geo_feats]` → single vector  
   - Pass through a small MLP head: Linear → ReLU → Dropout → Linear → tags  
   - Input dimension = 512 (image) + 512 (text) + 2 (geo) = 1026

2. **Branch MLP + Sum + Normalize**  
   - Independently project each modality into a shared 512-dim space via MLPs  
   - L₂-normalize each branch, sum: `fused = normalize(img_proj + txt_proj + geo_proj)`  
   - Final classifier: Linear(512 → 49)

## 📁 Repository Structure
