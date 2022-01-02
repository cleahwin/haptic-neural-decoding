# Modeling the Human Haptic Code

## Abstract
Approximately 300 million people are in need of wearing prosthetic limbs. However, current prosthetics offer limited tactile experience. In my project, I perform a systematic study of the brain’s representation of touch by decoding electroencephalography (EEG) recordings of neural activity to predict objects a person is exploring using certain sensory modalities. I collected EEG data using a non-invasive, compact Muse headband with three electrodes while participants explored four pairs of objects, each with opposing tactile features. Participants were asked to touch an object without viewing it, touch an object while viewing it, and imagine touching an object while viewing it. I used logistic regression, k-nearest-neighbors, and a multilayer perceptron to predict tactile features given EEG data. My models were relatively accurate in classifying responses to pairs of objects, with an average binary classification accuracy of 89%. When classifying eight objects, my models achieved an average accuracy of 56%, which is above chance (12.5%). I then performed recursive feature elimination to identify cortical regions and frequency bands that contribute most to the model’s accuracy. I found that regions in the temporal and parietal lobe contributed most to distinguishing these changes in multisensory integration states. In conclusion, I have demonstrated that opposing tactile features experienced by these modalities are strongly represented on the cortex. This localization and ability to classify responses to multiple touch types motivates future brain-computer interface research, perhaps even driving direct cortical stimulation feedback that mimics cortical signals during touch of objects with recordable tactile features. 

---
## Project Details
https://sites.google.com/view/modeling-haptic-code/home?authuser=0
### Rationale
Approximately 30 million people are in the need of wearing prosthetic limbs according to the World Health Organization. Prosthetics are designed to restore the normal function of a missing body part. However, current prosthetic limbs typically do not enable realistic tactile sensation (e.g., sense of soft/rough, hot/cold.) One reason for this is the challenge in converting tactile features, such as temperature and roughness, into neural activity that can be evoked through stimulation of the brain. Neural activity can be measured using a technique called electroencephalography (EEG). My project aims to create Machine Learning (ML) models that can generate neural activity that would enable an individual who cannot touch to perceive tactile labels (e.g. hot, rough). Neural-prosthetics can use these models to appropriately stimulate the brain to allow correct perception of tactile labels. Training these models is still challenging because of the inability to collect training data on the response to touch in individuals who have tactile deficits. I will also aim to develop vision based neuro-prosthetic training techniques for this purpose. I will also work towards developing a compact EEG-based brain-computer interface system that can control objects based on imagined touch.


### Research Goal
In this project I explore how visual and tactile sensation manifests in data from EEG brain sensors. I hypothesize that there is a correlation between neural activity and tactile features that are sensed through touch or vision. I aim to use this information to create models for tactile neuroprosthetics. There are three main goals in my project. First, I will predict tactile features of the object an individual is exploring given neural data recorded by a compact Muse headband. This would enable better understanding of how tactile and visual exploration of objects are encoded on the cortex, which may provide insights on developing brain-computer interfaces for various purposes. Second, I will develop models that generate new samples of EEG activity that could enable sensation of certain tactile features. This would be critical to a tactile prosthetic that stimulates the brain of an individual with tactile deficits in patterns that recreate perception of certain tactile features. Third, I will investigate the possibility of generating EEG signals to recreate touch based on EEG signals that enable visual exploration of certain objects. This would enable neuroprosthetic training in individuals with tactile deficits.

### Procedure
For this experiment, I recruited four participants. Because of the threat of COVID-19, I recruited family members that I have been living with since the start of the pandemic. I did not target any particular ethnic group, gender, race, or population. The age range of the participants is 10 - 50 years. First, the participant was asked to read and fill out the informed consent form. I made it clear that participation is fully voluntary and participants are allowed to stop or withdraw at any time. The participant is then fitted with a wireless Muse 2 headband. This was used to collect the EEG data for my experiment. I ensured that the participant is comfortable wearing the headband. The whole experiment was three parts and, in each part, the participant was presented with a series of eight objects (Figure 1 shows the four pairs: hot-cold, rough-smooth, firm-squishy, dry-wet). For the first part, the participant touched each object while their eyes were closed. For the second part, the participant looked at each object while imagining touching it. For the last part, the participant touched and looked at an object. These three conditions in which the participant was placed are described in Figure 2. There were four 10-second trials for each object separated by 10 second breaks (Figure 3). 
![image](https://user-images.githubusercontent.com/20733329/147862458-e5ff3c01-c93f-4f6f-b01d-f894ceb00623.png)

For collecting neural data, I used a Muse 2 headband. I connected the Muse headband to an app called Mind Monitor via bluetooth. This app records the data from the Muse and allows data to be exported as CSV files containing timestamps and signals from each electrode. All data was kept anonymous and confidential.

### Data Analysis
To preprocess the data, I removed time points where collected values were empty, zero, or undefined, as this represents poor quality of data collected by the Muse headband. I normalized the data and randomly split the data into 80% training and 20% testing sets. I decoded the labeled EEG data in order to better analyze the data. I created various binary classifiers, including logistic regression and a multi-layer perceptron, to analyze the differences in EEG activity associated with sensations of opposing touch types (e.g. hot vs. cold). For the coding in my project, I will use Python and Sci-kit libraries.

### Decoding Touched Tactile Labels
To model the neural code for various tactile features, I created binary, tertiary, and multiple classifiers which decode tactile labels of touched objects. I made three models: logistic regression, k-nearest-neighbors (kNN), and multilayer perceptron. I created a binary classifier which predicted one of two opposing tactile labels given the brain’s response to touch.
These confusion matrices visually show the accuracies of the models for the pair rough vs. smooth.
![image](https://user-images.githubusercontent.com/20733329/147862601-b3a6819e-2fda-42f3-8a74-33d1f8f6db39.png)
The vertical axis shows the actual label while the horizontal axis shows the predicted label. Since we would want the actual label to equal the predicted label, in general, the downward diagonal should be dark colored. The logistic regression model (Figure 4) had an accuracy of 84%, the kNN model (Figure 5) had an accuracy of 90%, and the multilayer perceptron (Figure 6) had an accuracy of 92%. These are all really high accuracies!

I also created a tertiary classifier (Figure 7) which predicted 3 tactile labels given the EEG response to touch.![image](https://user-images.githubusercontent.com/20733329/147862633-898fa01b-9666-4f1b-a992-ff18ccb1eb67.png)

This kNN model predicted hot, cold, or firm. The accuracy was 75%! Figure 8 shows the decision boundaries for this model. The dots represent data points and the colored regions represent the model’s prediction. The accuracy is quite high, so we would expect to see a fair separation in the data points labeled 'hot' versus the ones labeled 'cold'.

I also created a multiple classifier (Figure 9) which predicted all 8 tactile labels given the response to touch.
![image](https://user-images.githubusercontent.com/20733329/147862652-61ae7236-5abd-4c0b-b051-05c80b852d10.png)
The kNN model had an accuracy of 56%. Though this seems low, it is greater than 12.5% which would be the accuracy of the model if it were randomly guessing. 
It is amazing how these classifiers were able to accurately predict tactile features using a 3 electrode Muse headband! This all supports the existence of a clear code for different tactile labels accessible on the surface of the brain detectable by a Muse!

### Recursive Feature Elimination
To dig deeper, I aimed to identify the important features the models relied on, and hence the parts of the brain and their activity that contributes most to representing and evoking touch perception. I used 5 frequency bands at 3 locations on the cortex. I hypothesized that the brain would distinguish between different touch types in specific regions. Recursive feature elimination allowed me to understand differences in cortical signaling under different senses and sensory integration of touch and vision. Recursive feature elimination (Figure 10) works by recursively removing features and tests the model’s without them. This would tell which features contributed most to the model’s accuracy.
![image](https://user-images.githubusercontent.com/20733329/147862764-1f3a3691-26dd-449f-bc3a-0c4a27b814f2.png)

The first heatmap (Figure 11) is for touch, the second (Figure 12) is for imagined touch with vision, and the third (Figure 13) is touch with vision. Darker colors indicate  that that feature contributed more to the accuracy of the model. For touch, Delta and Beta TP10 were the most important. For imagined touch and vision, Delta TP10 and Gamma AF8 contributed the most, and for touch with vision, Theta TP9 and Gamma TP10 were the most important.

From this, TP9 and TP10 were the most important for the majority of modalites. These are electrodes found in the temporal and parietal regions. This is very exciting because these regions are actually involved in sensation, indicating that this area is a target for stimulation based sensory restoration.

### Conclusion
Here are the main takeaways from my project:
1) Responses of the brain to touch of different objects can be clearly mapped at three electrode locations on the Muse headbands
2) Machine learning models can accurately capture the brain’s representation of touch and classify EEG-recorded responses of the brain to imagination and vision of up to eight different objects.
3) Electrodes near the temporal/parietal lobe are especially important for discriminating responses, pointing to this region as the critical site of multisensory integration.

### Future Work
In the future, I would like to improve my data collection by increasing the number of participants and trials per participant. I would also like to  use variational autoencoders to predict the brain’s response to certain tactile labels. Although it may be difficult to test without invasive brain stimulation, this would be useful because the brain could be stimulated in certain ways to evoke responses. Additionally, I would like to utilize transfer learning and see if the brain’s response to certain tactile labels vary among people. 

---
## Acknowledgments
I would like to thank Courtnie Paschall (MD/PhD Student at the University of Washington) for mentoring me through the course of my project. I am also grateful to my family who participated in my experiment and supported me through this project.

---
## Files
Here is a brief description of the main files you will find in this repository:
- ``models_and_plots.ipynb`` contains the main code that I wrote. This Jupyter notebook includes all the training and testing of binary classifiers, multiple classifiers, and neural networks. I used confusion matrices (also known as heat maps) to represent the results from these models. Additionally, this file includes various tools I used to analyze my data: recursive feature elimination, prinicpal component analysis, and t-distributed Stochastic Neighbor Embedding.
- ``cvae.ipynb`` is my attempt in using a Conditional Variational Auto-Encoder to predict the EEG data of an individual given a certain sensation task. It achieved an accuracy of ~50% which is poor. Future work may attempt to improve the features or setup of the model.
- ``lab_book.pdf`` contains slides I created as I worked on this project documenting my progress. It includes plots, tables, experimental designs, flowcharts, and questions.
- ``project_poster.png `` is the poster I presented at the 2021 *Central Sound Regional Science & Engineering Fair* (CSRSEF) and the *Washington State Science & Engineering Fair* (WSSEF). It won second place at the CSRSEF and a first place at the WSSEF.
