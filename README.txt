#Readme

#Project Description
This project focuses on frame-level speech recognition, where the goal is to predict phonemes for each frame of an audio signal. Using Mel-Frequency Cepstral Coefficients (MFCC) as features, we aim to develop a machine learning model capable of recognizing phonemes in spoken language. This task is crucial for various speech-related applications, such as automatic speech recognition systems and voice assistants.

#Requirements:
Given in the requirements.txt file.

#Dataset Description
The dataset consists of pre-extracted MFCC features and corresponding phoneme labels. It is divided into three subsets:
train-clean-100: Used for training the model.
dev-clean: Used for validation and hyperparameter tuning.
test-clean: Used for final model evaluation.

Each frame of the dataset is represented by a vector of 28 features derived from MFCC analysis. The corresponding labels indicate the phoneme spoken at each time step.
https://www.kaggle.com/competitions/11785-spring-25-hw-1-p-2

#WandB Link:
https://wandb.ai/IDL_785/IDL_HW1P2

#Features
- Frame-level speech recognition using MFCC features.
- Prediction of phonemes based on mel spectrogram representations.
- Implementation of context windowing to improve phoneme classification accuracy.
- Evaluation using phoneme classification metrics.

#Final Model
Archetype: inverse-pyramid   
Parameters: 19.75M  
Number of layers: 28  
Activation function: Mish (Reference: https://arxiv.org/vc/arxiv/papers/1908/1908.08681v1.pdf)  
Model Train time: 4 hours 30 mins

#Experiments and Abalations
For HW1, I hardcoded a lot of the hyperparameters instead of updating them and using them directly from config. I will make sure to not repeat this mistake starting HW2. This is the reason you will a lot of repeated hyperparameters in my wandb summary. I have tried mentioning the ones I actually used and remember in the abalations description below, however, not all of them were documented.

##Abalations 1-5
Architecture: Diamond    
Activation function: GELU   
Model Train time: 2-4 hours   
Batch Size: 2048/4096   
Scheduler: ReduceLROnPlateau    
Optimizer: SGD   
Epochs: 15     
These were the intial few abalations I tried where the goal was only to cross the 60% mark. I was able to reach 82-83% with my architecture and not changing a lot of the parameters provided.

##Abalations 6-10
Architecture: Diamond/pyramid/inverse-pyramid         
Activation function: GELU     
Model Train time: 1-2 hours       
Batch Size: 4096/8162     
Scheduler: ReduceLROnPlateau       
Optimizer: AdamW/SGD      
Epochs: 10/15/60         
After understanding the homework a little more, I tried playing around with the parameters. I tried working with different structures, learnt why we should experiment with different batch sizes and run more epochs than just 10-15.However, I was only able to reach 84% cutoff.

##Abalations 11-15
Architecture: Diamond/pyramid/inverse-pyramid        
Activation function: GELU / Mish    
Model Train time: 1-2 hours      
Batch Size: 4096     
Scheduler: ReduceLROnPlateau/CosineAnnealing      
Optimizer: AdamW      
Epochs: 10/15/60       
Working with my study group members and others in our class, I tried using a different activation function - Mish which started giving me better results. (Didnt not change it in config which is why in wandb it still shows GELU). Also, change the scheduler I was using to use CossineAnnealing (as it smoothly reduces the LR, preventing sudden drops). This also helped my model perform better.

##Abalations 16-20
Architecture: inverse-pyramid     
Activation function: Mish     
Model Train time: 4-6 hours     
Batch Size: 4096     
Scheduler: CosineAnnealingWarmRestarts      
Optimizer: AdamW     
Epochs: 30/45      
Finally, the last few abalations I ran, I was able to get to 85% accuracy. After trying different architecture I realized inverse-pyramid was working best for me based on the parameters that I was using. I tried a lot of different combinations for this structure. I increased my training time to 4-6 hours and ran more epochs to give my model the time to actaully learn from the training data.


#Acknowledgment
- I would like to acknowledge my study group members: Yukta Bhartia and Swastik Chowdhury for helping me reach the 85% accuracy by suggesting architectural changes
- I would like to acknowledge Aditya Sannabhadti who suggested the usage of the Mish function