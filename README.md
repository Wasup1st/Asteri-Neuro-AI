# Asteri Neuro AI

An active medical research project focused on using 3D Convolutional Neural Networks (3D-CNNs) to detect Alzheimer's Disease (AD) from MRI scans.

## The Journey

### Phase 1: The Baseline
* Built a custom data loader to process 225 raw 3D NIfTI MRI scans into uniform 128x128x128 blocks.
* Trained a standard 3D-CNN baseline model.
* **Result:** Achieved 64.44% accuracy, but generated Saliency Maps proved the model was "cheating" by focusing on the high-contrast edges of the skull and background noise rather than actual brain tissue.

### Phase 2: The Neurology Optimization (Current)
To make the model scientifically valid, the AI needed to be forced to study internal brain structures. Phase 2 focused on cleaning the medical data and engineering solutions to bypass hard RAM limits during 3D processing.
* **Skull Stripping:** Built a computer vision preprocessor using Connected Component Analysis to physically remove the skull and isolate the gray/white matter.
* **Data Augmentation:** Multiplied the clean training data using mirrors and 5-degree tilts to prevent the model from memorizing specific patients.
* **The Drip-Feed Generator:** Engineered a dynamic data generator that feeds exactly one augmented patient to the AI at a time, keeping RAM usage near zero.
* **Lightweight Architecture:** Rebuilt the 3D-CNN with strided layers to instantly compress the math footprint by 8x.
* **Result:** 55.56% real-world accuracy on a locked test vault. Phase 2 Saliency Maps confirm the AI is now correctly targeting the ventricles and internal tissue instead of the bone. 

## Next Steps
* Transition to dedicated GPU hardware to train the uncompressed data over thousands of epochs.
* Resolve stride-induced checkerboard artifacts to push diagnostic accuracy higher.
