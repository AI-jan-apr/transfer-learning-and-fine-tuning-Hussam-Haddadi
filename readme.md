Food-11 Classification Project README
1. Dataset Description
Source: Food-11 Image Dataset
Classes: 11 categories (Bread, Dairy product, Dessert, Egg, Fried food, Meat, Noodles-Pasta, Rice, Seafood, Soup, Vegetable-Fruit).
Structure:
training/: 9,866 images
validation/: 3,430 images
evaluation/: 3,347 images
Total Images: 16,643
2. Preprocessing Pipeline
Resolution: All images resized to 224x224 pixels.
Normalization: Pixel values rescaled to the [0, 1] range.
Optimization: Used tf.data API with prefetch and AUTOTUNE for high-speed training.
3. Training Strategy
Stage 1: Feature Extraction
Base Model: EfficientNetB0 (ImageNet weights).
Layer Status: Base layers frozen.
Top Layers: GlobalAveragePooling2D -> Dropout(0.2) -> Dense(11, Softmax).
Epochs: 5
Stage 2: Fine-Tuning
Layer Status: Base layers unfrozen.
Optimizer: Adam with a very low learning rate (1e-5).
Goal: Adapt pre-trained features to specific food nuances without destroying general knowledge.
Epochs: 5
4. Key Findings
Convergence: Fine-tuning significantly reduced the validation loss compared to simple feature extraction.
Generalization: The gap between training and validation accuracy remained stable, suggesting good generalization across the 11 food classes.