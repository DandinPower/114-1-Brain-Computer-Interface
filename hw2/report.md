# Brain-Computer Interface HW2: EEG Analysis

414551003 廖永誠

## Multiple Choice

### Problem 1

When averaging **k** single trials to obtain a final ERP waveform, the ERP **signal** is time locked and consistent across trials, so averaging does **not** change its amplitude, the signal stays the same as in a single trial. In contrast, the background EEG **noise** is random and uncorrelated across trials, so its amplitude is reduced by a factor equal to the *square root of the number of trials*, that is, it becomes the single trial noise divided by √k.

The initial **signal to noise ratio (SNR)** is 5 µV divided by 10 µV, which is 1 over 2. After averaging k trials, the SNR becomes the original SNR multiplied by √k. We want the final SNR to be 2, so we set the desired SNR, 2, equal to the original SNR, 1 over 2, times √k, and solve for k. This gives √k = 4, so k = 16. Therefore, we need to average **16 trials**, and the correct option is **(C) 16**.


### Problem 2

Because (A) PCA reduces dimensionality by finding principal components that capture the most variance in the data, without using class labels. And (D) ICA separates mixed signals into statistically independent componenets. (E) K-means groups data into clusters based on similarity, also without labels. So The correct option are **(A) PCA, (D) ICA and (E) K-means clustering**. 

### Problem 3

The first correct option is (C) The Same as the Number of EEG Channels. Because this is the maximum possible number of components i can extract without adding more channels. But also if the hypothesis is the actual number of true independent brain sources contributing to the EEG signal is less than the number of recorded channels (N) and think that only there are K principal components account for. The ICA can project the data onto those K components. So (E) might also right. So The correct option are **(C) The same as the number of EEG channels and (E) As many as the number of independent brain sources**.

## Programming Problems

### Problem 1-1

1. Plot 2D channel location map

    ![problem1_1_2d_channel_location](images/problem1_1/problem1_1_2d_channel_location.png)

2. Run ICA and record the computational time of ICA by code.

    - ICA computation time: 22.80 seconds

3. Plot component maps in 2D.

    ![problem1_1_components_plot_1](images/problem1_1/problem1_1_components_plot_1.png)

    ![problem1_1_components_plot_2](images/problem1_1/problem1_1_components_plot_2.png)

    ![problem1_1_components_plot_3](images/problem1_1/problem1_1_components_plot_3.png)

4. Indicate noise component(s) if they exist and explain the reason why you identify this component as noise or artifact.

    The detail peaked artifacts is demonstrate in problem2.ipynb, since different type of artifacts have similar pattern, here i peak some components in report to provide the reason.

    1. EMG like component
        
        ![problem1_1_emg_like](images/problem1_1/problem1_1_emg_like.png)

        The topography is diffuse, the time courses are fast and noisy without clear event locking, and the spectrum has strong high frequency power toward 100 Hz, which is typical of muscle tension rather than cortical EEG, so it is suitable to remove as muscle artifact.
        
    2. ECG like component
        
        ![problem1_1_ecg_like](images/problem1_1/problem1_1_ecg_like.png)

        The topography is diffuse and non focal, the segment image shows repeated, stereotyped deflections in the same latency range across segments, and the spectrum has a clear low frequency peak around the heart rate rather than a typical neural rhythm, so it is suitable to remove as cardiac contamination.
        
    3. Line noise like component
        
        ![problem1_1_line_noise](images/problem1_1/problem1_1_line_noise.png)

        The spectrum shows a sharp, isolated peak around 50 Hz, the time courses are dominated by stable high frequency oscillations that repeat across all segments, and there is no clear event related pattern, so it is a good candidate for removal.
        

5. Plot the first 10-second channel data before and after deleting noise/artifact component(s).
    - before
       
        ![problem1_1_before_deleting](images/problem1_1/problem1_1_before.png)
    - after
       
        ![problem1_1_after_deleting](images/problem1_1/problem1_1_after.png)

    After removing the noise/artifact ICs, the first 10-second EEG segment becomes visibly cleaner: high frequency, irregular fluctuations and large transient spikes are reduced, especially in frontal and temporal channels, and the remaining signals show smoother, more consistent rhythms. This suggests that ICA successfully suppressed non-neural artifacts while preserving the overall EEG pattern.

### Problem 1-2

1. Plot 2D channel location map

    ![problem1_2_2d_channel_location](images/problem1_2/problem1_2_2d_channel_location.png)

2. Plot spectra and map in 2D.

- spectral
    ![problem1_2_spectral](images/problem1_2/problem1_2_spectral.png)

- 2d
    ![problem1_2_spectral_2d_map](images/problem1_2/problem1_2_spectral_2d_map.png)

3. Plot the first 10-second channel data, and discuss anything you observed.

    ![problem1_2_first_10_secs](images/problem1_2/problem1_2_first_10_secs.png)

    In this 10 second segment, the frontal channels Fp1 and Fp2 show large, slow drifts and a few sharp deflections with amplitudes close to the 200 µV scale bar. These slow and high amplitude changes are much stronger than what we usually expect from cortical activity and are typical of eye related artifacts, for example blinks or slow eye movements picked up by the frontal electrodes which fit the dataset i used (i choose the open not closed .csv for this problem). The overall waveform looks relatively low frequency and nonstationary.

    In contrast, the occipital channels O1 and O2 have smaller amplitudes and contain faster oscillations. Their activity looks more stable over time and includes a visible rhythmic component that is roughly in the alpha range, which is consistent with the alpha peak and posterior dominance seen in the spectral plot and 2D spectral maps. The comparison between frontal and occipital channels therefore suggests that frontal sensors are heavily contaminated by ocular activity, while the occipital sensors reflect cleaner ongoing EEG with stronger alpha and higher frequency components.


### Problem 2

1. Plot 2D channel location map
    
    ![problem2_2d_channel_location](images/problem2/problem2_2d_channel_location.png)
2. Bandpass filtering [1, 48]Hz.
    
    ![problem2_bandpass_filtering_plot](images/problem2/problem2_bandpass_filtering_plot.png)

3. Run ICA and record the computational time of ICA by code.
    - ICA computation time: 59.15 seconds

4. Plot component maps in 2D.
    ![problem2_components_plot_1](images/problem2/problem2_components_plot_1.png)
    ![problem2_components_plot_2](images/problem2/problem2_components_plot_2.png)
    ![problem2_components_plot_3](images/problem2/problem2_components_plot_3.png)

5. Indicate noise component(s) if they exist and explain the reason why you identify this component as noise or artifact.

    The detail peaked artifacts is demonstrate in problem2.ipynb, since different type of artifacts have similar pattern, here i peak some components in report to provide the reason.
    
    1. EMG like component
        
        ![problem2_component_emg_like](images/problem2/problem2_component_emg_like.png)

        This component shows broad band high frequency activity with irregular fast bursts over the frontal and temporal edges, which matches the typical pattern of scalp muscle activity rather than cortical rhythms.
    2. ECG like component
        
        ![problem2_component_ecg_like](images/problem2/problem2_component_ecg_like.png)

        The topography is broadly distributed over the scalp, the segment image shows very regular, heartbeat-like deflections that repeat across almost all segments, and the spectrum has a strong low-frequency peak around the heart-rate range rather than a clear neural rhythm. Together, this pattern suggests volume-conducted cardiac activity rather than a localized brain source, so this component is a good candidate for removal.
    3. Line noise like component
        
        ![problem2_component_line_noise](images/problem2/problem2_component_line_noise.png)

        The spectrum shows a sharp, isolated peak around 50 Hz, the time courses are dominated by stable high frequency oscillations that repeat across all segments, and there is no clear event related pattern, so it is a good candidate for removal.



6. Plot the first 10-second channel data before and after deleting noise/artifact component(s).
    - before
       
        ![problem2_before_deleting](images/problem2/problem2_before_deleting.png)
    - after
       
        ![problem2_after_deleting](images/problem2/problem2_after_deleting.png)

7. Discuss the effect of bandpassing(highpassing) the signal before running ICA.

    Bandpass filtering the data from 1 to 48 Hz, especially the 1 Hz high pass, removes slow drifts and DC offsets and attenuates high frequency noise, so the input to ICA is more stationary and dominated by typical EEG rhythms. Compared with the raw signal, the filtered signal shows less baseline wander and clearer oscillatory structure, which helps ICA separate EMG, ECG, and line noise into cleaner independent components. The cost is that very slow neural activity and part of the true activity around 50 Hz are reduced, so the chosen passband needs to match the scientific goal.

### Problem 3

The preprocessing pipeline in steps 1 to 4 is implemented in `problem3.ipynb`.
Here I summarize step 5, where I compare four preprocessing methods at FCz.

---

#### 1. Without any operation

* SNR(error): **9.299**
* ERP plot

![problem3\_without\_any\_operation](images/problem3/problem3_without_any_operation.png)

**Figure description.**
Both correct and error trials show a clear feedback related response, with a large peak around 200 to 300 ms after feedback and additional slower fluctuations afterward. However, the waveform contains visible high frequency noise and slow drifts before time 0 and after time 600, which makes the baseline less stable.

**SNR interpretation.**
The SNR is already moderate, because the error ERP has a clear peak, but the baseline is relatively noisy. No preprocessing keeps both neural signal and artifacts, so the noise level in the pre stimulus period remains high.

---

#### 2. Bandpass only (1 to 48 Hz)

* SNR(error): **10.735**
* ERP plot

![problem3\_bandpass\_only](images/problem3/problem3_bandpass_only.png)

**Figure description.**
After bandpass filtering, the FCz waveforms become smoother. The pre stimulus interval is closer to a flat baseline and the main feedback related peak around 200 to 300 ms is preserved and even more clearly visible. Correct and error conditions still follow a similar shape but the peak for error trials stands out clearly.

**SNR interpretation.**
Bandpass filtering removes very slow drifts and high frequency noise while keeping most of the ERP energy in the typical 1 to 48 Hz range. This reduces the standard deviation in the pre stimulus interval more than it reduces the peak amplitude, so the SNR becomes the highest among the four methods. This suggests that simple bandpass filtering is very effective for this dataset.

---

#### 3. IC removal only

* SNR(error): **8.561**
* ERP plot

![problem3\_ic\_removal\_only](images/problem3/problem3_ic_removal_only.png)

**Figure description.**
After ICA based artifact removal, blink and muscle related fluctuations are reduced, and the main feedback response around 200 to 300 ms is still visible. However, the baseline before time 0 and after time 600 is not as stable as in the bandpass only condition, and some residual slow trends remain.

**SNR interpretation.**
ICA removes components labeled as muscle, EOG, ECG, line noise and channel noise. This helps remove some artifacts, but because the raw data are not filtered first, ICA has to deal with wideband signals that still contain slow drifts. In addition, automatic component rejection may remove a small part of the neural signal. As a result, both the peak amplitude and the baseline variance are affected, and the SNR becomes lower than in the bandpass only and even slightly lower than in the no preprocessing condition.

---

#### 4. Bandpass plus IC removal

* SNR(error): **5.975**
* ERP plot

![problem3\_bandpass\_ic\_removal](images/problem3/problem3_bandpass_ic_removal.png)

**Figure description.**
When bandpass filtering is combined with ICA, the waveforms look noisier and more irregular, and the clear feedback related peak around 200 to 300 ms is much less obvious. The correct and error traces overlap heavily and fluctuate around zero across the whole time window, including the post stimulus period.

**SNR interpretation.**
Here the pre stimulus noise is not much smaller than in the other conditions, but the peak amplitude of the error ERP is strongly reduced. This suggests that, after bandpass filtering, ICA may have removed components that also contained task related activity at FCz, not only artifacts. Because the signal of interest is reduced more than the noise, the SNR drops to the lowest value among all methods.

---

#### Summary of preprocessing effects

Overall, the results indicate that a simple bandpass filter is sufficient and even preferable for enhancing the error ERP at FCz in this recording, while more complex ICA based cleaning must be tuned carefully to avoid removing meaningful neural components.
