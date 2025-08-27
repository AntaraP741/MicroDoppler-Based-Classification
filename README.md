# MicroDoppler-Based-Classification
Introduction
The classification of small UAVs (sUAVs) has gained significant attention due to their increasing use in civilian and defense applications. Traditional vision-based methods, such as RGB/thermal imaging and shape recognition, face challenges in low-light, cluttered, or occluded environments. Similarly, acoustic and RF-based detection systems often struggle with noise, interference, and limited range.  
In contrast, radar-based micro-Doppler signatures capture fine motion characteristics (e.g., blade rotations, wing flapping), which are highly discriminative for identifying UAV types in real-world conditions.
Current Methods for sUAV Classification
1. RGB/EO-IR Cameras – Effective in clear conditions, but suffer from lighting dependence and line-of-sight requirements.  
2. Acoustic Sensors – Can identify drones by their rotor sound but fail in noisy urban or battlefield environments.  
3. RF Signature Analysis – Works when drones actively transmit signals but ineffective against autonomous or stealthy UAVs.  
4. Radar with Micro-Doppler – Independent of lighting/weather, captures motion patterns of UAV blades/wings, and provides strong separability across classes.

Proposed Approach: Micro-Doppler Based Classification
We trained a deep learning model on Micro-Doppler radar spectrograms of 5 classes: Bird, Drone, Long_Blade_Rotor, Short_Blade_Rotor, and RC_Plane. The model was trained for 10 epochs, with both training and validation accuracies stabilizing near 94–95%.

Dataset

The dataset used in this study is the DIAT-µSAT Micro-Doppler Signature Dataset, sourced from IEEE DataPort (https://ieee-dataport.org/documents/diat-msat-micro-doppler-signature-dataset-small-unmanned-aerial-vehicle-suav). It contains 4,849 micro-Doppler spectrogram images of small unmanned aerial vehicles (SUAVs), including RC planes, long-blade rotors, short-blade rotors, drones, and birds. The dataset is designed to capture variations in revolution per minute (200–1740 RPM), flapping rates (2–4 flaps/s), azimuth angles (0°–360° in steps of 45°), and elevation angles (0°–90° in steps of 30°). This diversity makes it a robust benchmark for real-world UAV detection and classification.
Methodology
For classification, we employed ResNet-18, a deep residual convolutional neural network (CNN). ResNet-18 was chosen because of its balance between computational efficiency and representational power. The residual connections in ResNet mitigate the vanishing gradient problem, allowing deeper networks to be trained effectively. This makes it especially suitable for micro-Doppler spectrogram classification, where subtle motion patterns must be captured.

The model was fine-tuned on the DIAT-µSAT dataset, with spectrogram images resized to 224x224 and normalized. We used transfer learning, initializing ResNet-18 with pre-trained ImageNet weights and retraining the final layers to adapt to the five target classes: Bird, Drone, Long_Blade_Rotor, RC_Plane, and Short_Blade_Rotor. The Adam optimizer was used with a learning rate schedule, and the model was trained for 10 epochs with 80/20 train-validation split.

