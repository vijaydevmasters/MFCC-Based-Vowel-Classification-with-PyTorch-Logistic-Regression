```markdown
# Logistic Regression for Vowel Classification in PyTorch

**Overview**
--------

This project implements a logistic regression model using PyTorch, trained with stochastic gradient descent (SGD), to perform binary classification of American English vowels. The model is applied to differentiate between pairs of vowels spoken in 'hVd' (e.g., "had", "hid") contexts, using the Hillenbrand et al. (1995) dataset.

The system processes WAV audio files by:
1.  Extracting 13-dimensional Mel-Frequency Cepstral Coefficients (MFCCs) using the `librosa` library.
2.  Selecting the middle frame of each utterance's MFCCs as its representative feature vector.
3.  Normalizing these features (z-scoring) across the entire dataset.

The logistic regression model then learns to classify user-specified pairs of vowels (e.g., 'iy' vs. 'ah', 'eh' vs. 'ae'). The classification difficulty, and thus test accuracy (ranging from 0.5 to 1.0), varies depending on the acoustic similarity of the chosen vowel pair.

**Key Features**
-------------

*   **Audio Feature Extraction:** Utilizes `librosa` to compute MFCCs from raw audio signals, focusing on the temporal midpoint of vowel utterances.
*   **Data Preprocessing:** Implements z-score normalization for feature scaling, ensuring robust model training.
*   **PyTorch Model:** A logistic regression model built with a single `nn.Linear` layer and a sigmoid activation function.
*   **Training:** Employs Stochastic Gradient Descent (SGD) for model optimization, with explicit gradient zeroing, forward pass, loss calculation, and backpropagation steps.
*   **Vowel Pair Customization:** Allows users to select any two vowels from the dataset for binary classification.
*   **Dataset:** Leverages the Hillenbrand et al. (1995) vowel dataset, which includes utterances from men, women, and children.

**Dataset Vowels:**
The following vowels from the dataset can be used for classification:
`ae, ah, aw, eh, ei, er, ih, iy, oa, oo, uh, uw`

**Setup & Installation**
--------------------

1.  It's recommended to create and activate a Python virtual environment:
    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Unix/macOS
    # venv\Scripts\activate  # On Windows
    ```

2.  Install the required Python packages:
    ```bash
    pip install -r requirements.txt
    ```

**Running the Classification**
---------------------------

The main script `lr_speech.py` can be run from the command line. You need to specify the two vowels to classify.

**Usage:**
```bash
python lr_speech.py --vowels <VOWEL1>,<VOWEL2> [OPTIONS]
```

**Example:**
To classify between the vowels 'ih' and 'eh':
```bash
python lr_speech.py --vowels ih,eh
```

**Available Options (see `python lr_speech.py --help` for more):**
*   `--directory`: Path to the Hillenbrand dataset directory (default: `./Hillenbrand`).
*   `--num_mfccs`: Number of MFCCs to extract (default: 13).
*   `--passes`: Number of training epochs (default: 5).
*   `--batch`: Batch size for training (default: 1).
*   `--learnrate`: Learning rate for SGD (default: 0.1).

**Potential Enhancements**
----------------------
While MFCCs from the midpoint frame provide a good baseline, alternative feature extraction strategies could be explored to potentially improve classification performance on more acoustically similar vowel pairs. This could include:
*   Averaging MFCCs over several frames or the entire vowel duration.
*   Using delta and delta-delta MFCCs to capture dynamic information.
*   Exploring other acoustic features like Formants, Pitch, or LPC coefficients.

**References**
------------

Hillenbrand, J., Getty, L. A., Clark, M. J., and Wheeler, K. (1995). Acoustic characteristics of American English vowels. *Journal of the Acoustical Society of America, 97*(5):3099–3111.
```
