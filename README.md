# Multimodal-MRS-Master-Thesis
Creating a multimodal (audio-lyrical) and comparing it with a unimodal MRS (audio-only) in the next-track recommendation tasks.

# About the Project
This project is a Master Thesis created by Jelena Kalinic, a Behavioural Data Science student at the University of Amsterdam. The project was supervised by Dr. Michael Nunez. 

# Abstract
With an increasing amount of digital music released daily, streaming platforms such as Spotify face the following issue: how to develop the best music recommendation systems (MRSs) to increase user experience? This study aimed to address the semantic gap in MRS literature by incorporating both audio and lyrical information in a deep learning multimodal approach. Two networks were trained on genre classification of the songs from a custom-created dataset: an audio-only input network using CNN architecture and a multimodal network using both audio and lyrics input, which incorporates a combined CNN and BERT architecture. Then, from each trained network, a MRS was created. Lastly, a computer-based experiment was conducted with two participants to compare recommendations generated by the two MRSs. In the experiment, a random song recommendation was played and the participants stated whether they liked the song. If they did, the liked song acted as an anchor, based on which songs generated by the audio-only MRS, multimodal MRS, and a control song were played in random order and evaluated. The control song was randomly chosen from the whole dataset for Participant 1 and from the same genre as the anchor song for Participant 2. Results suggest a 7% increase in performance in genre classification accuracy of the multimodal model over the audio-only model. The power of the experiment did not allow generalization on a population level, but found a preference for recommendations generated by the multimodal MRS in the second participant though not in the first. This study shows the benefits of a multimodal approach for creating MRSs and lays out an easily extendable methodology for future experiments with large sample sizes.

# Data
The data collection began by downloading the “5 Million Song Lyrics Dataset” from Kaggle (Nayak, 2022; https://www.kaggle.com/datasets/nikhilnayak123/5-million-song-lyrics-dataset). The dataset has 9.21 GB and contains metadata of 5 million songs across six genres: rap, pop, country, rock, metal, and RnB. The metadata includes the songs’ lyrics, genre tag, number of views of the lyrics on Genius, artist name, title, song ID,  and release year. Due to this extremely large capacity, a subset of only the top most viewed songs across four genres, namely: rap, pop, country, and rock, were used to train and evaluate the models and MRSs.

Using the ‘spotdl’ library in Python (https://spotdl.readthedocs.io/en/latest/), each of the songs from the chosen subset of the dataset was downloaded from YouTube music with their corresponding titles. Since ‘spotdl’ was not able to find all of the queried songs on YouTube, additional songs were fetched from the original “5 Million Song Lyrics Dataset” dataset. The songs are stored in mp3 file format once downloaded with the title provided on YouTube music. It is important to mention that the downloaded titles of the songs from YouTube music using “spotdl” were not an exact mapping of the titles in the “5 Million Song Lyrics Dataset”. Thus, a custom function was created to link the downloaded songs back to their corresponding titles in the lyrics dataset, but also to remove instances where the song was not downloaded at all. Only songs with lyrics in English were retained. This was accomplished by using an in-built function in Python that detects non-English words. Nonetheless, the function does not remove all of the songs with complete accuracy, thus the process also required manual removal of the songs. The additional preprocessing and cleaning resulted in 4550 songs per genre, yielding the total dataset of 18200 songs.

The dataset couldn't be uploaded due to *copyright* issues. Contact this GitHub profile if you want the custom-created dataset used in this study.

# How to execute this project

First run the ```cut_audio.py``` script to cut the songs into 30-second snippets. Then, proceede with creating and slicing spectrograms of the audio snippets, ```make_spectrograms.py```, ```cut_spectrograms.py```.

Second, go to Google Collab and open the ```Models_Thesis.ipynb``` to run the audio-only and multimodal model. Turn on the GPU option in Google Collab for faster processing. Save the computed vectors onto the Google Drive and download them to continue the project locally.

Next, on your local computer, start creating the recommendation systems in the following order: ```recommendations_audio.py```, ```recommendations_multi.py```, ```recommendations_random.py```, ```recommendations_genre.py```. To check how many recommendations from audio-only and multimodal MRS were the same run ```check_recommendations.py```. To combine all of the recommendations for the experiment, run ```all_recommendations.py```.

Lastly, to make the experiment the audio files need to be cut again into 10-second snippets. For that run ```ten_sec_audio.py```, run the experiment on participant 1 and participant 2 with ```experiment_1.py``` and ```experiment_2.py```.

# Additional 

If you want to check or create a power simulation analysis, check ```power_simulation.py``` to get the power estimates (for this study) when making conclusions about a single participant and ```power_simulation_future.py``` to get the power estimates (a future recommendation) when making conclusions about the population (with more participants possible). 

If you want to make plots from the trained models, run ```graph_audio.py``` and ```graph_multi.py```. The scripts contain code to create the accuracy and loss graphs (training versus validation test set), and the confusion matrices to compare the genre classification. 


# Preview of the Methods and Network Structures to make the MRS

## The Multimodal Model (Audio-Lyrical) Architecture

![Thesis_Model drawio-2](https://user-images.githubusercontent.com/94328819/187284010-fb9f5e30-47b3-417b-9ef1-f7599a8a1ff2.png)

## Creating an MRS from the Audio-only model 
Inspired by Shenoy(2019) and his repository (https://github.com/VikramShenoy97/Music-Recommendation-Using-Deep-Learning)

![Recommendation drawio-2](https://user-images.githubusercontent.com/94328819/187284344-2ddc9b08-8563-499c-b65e-adf6087e25e0.png)





