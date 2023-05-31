# CFAR README

The provided code implements a 2D Constant False Alarm Rate (CFAR) technique, which is used in radar signal processing to detect targets in a noisy environment. The code follows these steps:

**Implementation steps for the 2D CFAR process:**
* The entire 2D range-Doppler map is processed by sliding a window across the map.
* For each Cell Under Test (CUT) in the window, the average noise level is calculated from the surrounding training cells. Training cells are a set of cells surrounding the CUT which do not include the guard cells and are used to estimate the noise level.
* The threshold is set as the noise level offset by a certain Signal to Noise Ratio (SNR) value.
* The signal level of the CUT is compared to this threshold. If the signal level is greater than the threshold, the CUT is flagged as containing a target (assigned a value of 1). Otherwise, it's assigned a value of 0, indicating no target.

**Selection of Training, Guard cells and offset:**
* The training cells n_t_cells and n_t_bands are chosen in both dimensions, here as 8 cells in range and doppler dimensions respectively.
* The guard cells n_g_cells and n_g_bands are also chosen in both dimensions, which in this case is 4 cells in range and doppler dimensions respectively. Guard cells are the cells around the CUT that are not used in noise estimation to avoid the risk of including target cells into the noise estimate.
* The offset is set to 1.5 dB. This is the value added to the averaged noise level to calculate the threshold.

**Steps taken to suppress the non-thresholded cells at the edges:**
* When sliding the window across the range-Doppler map, the loop's start and end points are adjusted to avoid the edges. The window is only moved across cells where the entire window (including training and guard cells) fit within the range-Doppler map.
* By doing this, cells at the edges (where the window cannot fully fit) are automatically suppressed, as they will not be considered as potential CUTs.