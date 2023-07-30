# Transfer Learning with MobileNetV2 - Alpaca/Not Alpaca Classifier

This project demonstrates the application of transfer learning using the MobileNetV2 model to build an Alpaca/Not Alpaca classifier. The purpose of this project was to create a deep learning model that can differentiate between images of alpacas and images of objects that are not alpacas. The project was undertaken as part of the Coursera Deep Learning Specialization.

## Dataset Creation and Splitting

The first step involved in this project is to create a suitable dataset and split it into training and validation sets. The `image_dataset_from_directory` function from the TensorFlow (`tf.keras.preprocessing.image`) library was utilized for this task. This function is particularly useful for image classification tasks where the images are organized in separate subdirectories based on their respective classes.

## Data Preprocessing and Augmentation

To enhance the training dataset's diversity and size without acquiring additional real-world data, data augmentation techniques were applied. Data augmentation involves applying various transformations to images, such as rotations, flips, translations, scaling, brightness adjustments, etc. This process generates new variations of the original data, making the model more robust and less prone to overfitting.

## Importing the Pretrained MobileNetV2 Model

The MobileNetV2 model was employed in this project, but before using it, the input images needed to undergo preprocessing to ensure they were in the correct format and range. A specific preprocessing function was utilized to prepare the input images according to the MobileNetV2 model's requirements for inference.

## Layer Freezing with the Functional API

The first approach to adapting the pretrained model for the new classifier task was performed through three main steps:

1. Deletion of the top layer: The top layer of the MobileNetV2 model, which was designed for the original classification task, was removed.
2. Addition of a new classifier layer: A new classifier layer was added to the model, allowing it to recognize alpacas as a new class.
3. Freezing the base model: The weights of the base MobileNetV2 model were frozen, meaning they were not updated during training. Only the newly-created classifier layer was trained during this phase.

The model was then compiled and trained for 5 epochs using this approach.

## Fine Tuning

The initial performance of the model was satisfactory, but to further improve its accuracy, a technique called fine-tuning was employed. Fine-tuning involves updating some of the weights in addition to the last output layer. The intuition behind fine-tuning is to allow the network to adapt its high-level features to the new data while keeping the low-level features (learned from the original task) intact.

To implement fine-tuning, the final layers of the MobileNetV2 model were unfrozen, allowing them to be updated during training. The optimizer was re-run with a smaller learning rate to fine-tune the high-level features for better recognition of alpaca-specific characteristics like soft fur or distinctive features.

By incorporating fine-tuning, the model's ability to detect and distinguish alpacas from other objects is expected to be significantly enhanced.

---

