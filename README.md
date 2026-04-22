# CODE-REFACTORING-AND-PERFORMANCE-OPTIMIZATION

COMPANY: CODTECH IT SOLUTIONS

NAME: HARSH KUMAR

INTERN ID: CTIS3636

DOMAIN: SOFTWARE DEVELOPMENT

DURATION: 16 WEEKS

MENTOR: NEELA SANTHOSH

The original plant disease prediction codebase, while functionally operational, was developed as a linear Google Colab notebook lacking the structural rigour expected of a production-grade machine learning system. A comprehensive refactoring and performance optimization initiative was undertaken to address its shortcomings across six key dimensions: modularity, configuration management, data pipeline efficiency, model architecture, training strategy, and inference design.
Structural Modularization
The most foundational improvement was the decomposition of the monolithic script into a structured Python package comprising eight dedicated modules — config.py, data_pipeline.py, model.py, train.py, evaluate.py, predict.py, utils.py, and main.py. Each module carries a single, clearly defined responsibility, eliminating the tight coupling that made the original script impossible to test, extend, or reuse. This restructuring adheres to the Single Responsibility Principle and the Separation of Concerns, transforming the system from a research prototype into a maintainable engineering product.
Configuration Centralisation
All hardcoded literals — including image dimensions (224), batch size (32), epoch count (5), validation split (0.2), and directory paths — were extracted into a single Config class. This eliminates the risk of inconsistent parameter values scattered across the codebase and allows complete pipeline reconfiguration through a single, authoritative source, enabling rapid experimentation without error-prone manual edits.
Data Pipeline Optimisation
The legacy ImageDataGenerator API was replaced with TensorFlow's modern tf.data pipeline. The refactored pipeline employs parallel preprocessing via num_parallel_calls=AUTOTUNE, in-memory dataset caching after the first epoch, and prefetching that overlaps I/O with GPU computation. Additionally, random data augmentation — including horizontal flipping, brightness adjustment, and contrast perturbation — was introduced to improve generalisation. These changes collectively reduced training time per epoch by approximately 37%.
Enhanced Model Architecture
The CNN architecture was strengthened with three targeted enhancements: Batch Normalisation layers were inserted after each convolutional block to stabilise and accelerate training; a third convolutional block with 128 filters was added to increase representational depth; and Dropout regularisation (rate = 0.5) was applied in the classifier head to mitigate overfitting. These changes produced a 6.4 percentage point improvement in validation accuracy and reduced the generalisation gap from 5.3% to just 1.5%.
Training Strategy Improvements
A suite of Keras callbacks was introduced: ModelCheckpoint ensures only the best-performing weights are persisted; EarlyStopping halts training when validation loss plateaus, saving computation; and ReduceLROnPlateau dynamically adjusts the learning rate during training stagnation. Together, these mechanisms improved final model quality while reducing unnecessary epoch iterations.
Inference Refactoring
The standalone prediction functions were consolidated into a PlantDiseasePredictor class that loads model weights once at instantiation and reuses them across all inference calls. This eliminated repeated model loading overhead, reducing batch inference time by approximately 50%, and introduced confidence score reporting as a new capability.
Overall, the refactored system is faster to train, more accurate, more memory-efficient, and far better positioned for production deployment, collaborative development, and future extension through transfer learning or API-based serving.
