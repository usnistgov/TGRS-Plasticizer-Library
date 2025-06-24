# Time Gated Raman Plasticizer Library

This library consists of time gated Raman spectra of 91 plasticizers included in the Scientific Polymer Products Inc. Plasticizer Kit$^‡$. The sample list can be found in the file: `SampleDetails.csv`. Plasticizers were measured at least in duplicate. Data was collected on a PicoRaman spectrometer (Timegate Instruments) using a 532 nm pulsed laser. The spectrometer was coupled through a fiber-optic probe (BAC102, B&W Tek). The wavenumber range of the measurements were calibrated using a polystyrene reference sample (PSRS) comparing the locations of 4 primary peaks at 620.9, 1001.4, 1031.8, 1602.3 $\textsf{cm}^{-1}$ (**McCreery 2000, Chap. 10**). Liquid samples were measured in aluminum sample pans, and solid samples were compacted using a pellet press. Sampling conditions were selected to minimize measured fluorescence and accompanying noise in the time-gated window. Parameters of laser power (mW) and collection time (s) were selected to achieve a Signal-to-Noise Ratio (SNR) exceeding 100. Collection times are reported in seconds and the Timegate software metric of sub acquisitions (SA), where samples were collected using 100 SA (13 s) or 300 SA (39 s). Some samples had significant fluorescence interference after time-gating and could not achieve an SNR >100. These samples are included in the library as is.
Specific information regarding the sampling conditions for each plasticizer are included in the file: `SampleDetails.csv`. The raw and processed data are also available at: https://datapub.nist.gov/od/id/mds2-3837.

###### To cite this Data:

Rieland, Julie M, Kotula, Anthony P, Migler, Kalman B, Beers, Kathryn L (2025), Time-gated Raman plasticizer library, National Institute of Standards and Technology, https://doi.org/10.18434/mds2-3837

----

### Data Calibration

During the data collection period, the instrument required repairs resulting in a change in the wavenumber set point of the detector and requiring different shift factors to calibrate the data, as documented in `SampleDetails.csv`. The unprocessed files (`SampleName_Raw.csv`) have not been adjusted with the PSRS calibration. 
The header lines of the unprocessed files include the peak locations of the PSRS that was measured during the same data collection session as the present sample and a calibration shift factor calculated using the method detailed below. The calibration shift is already incorporated in the processed data files (`SampleName_Proc.csv`), and further processing details can be found in the Jupyter Notebook accessible from the Github repository.

The calibration shift factor represents a weighted average of the deviation between the peak locations of the measured PSRS and standardized PS peak locations as reported in **McCreery 2000 Chap. 10**. Four peaks were assessed because the as-measured peaks presented some variation in their shifted position relative to the standardized peak locations. The average deviation of the peaks was calculated and weighted relative to the  corresponding peak intensities as reported in **McCreery 2000 Chap.10** (**Table 1**).

##### Table 1. Raman peak locations and relative intensities of polystyrene

|                                          | Peak 1 | Peak 2 | Peak 3 | Peak 4 |
| ---------------------------------------- | ------ | ------ | ------ | :----- |
| Standardized location [$\text{cm}^{-1}$] | 620.9  | 1001.4 | 1031.8 | 1602.3 |
| Weight                                   | 16     | 100    | 27     | 28     |

To calibrate the data, the calculated shift factor is scalar-added to the first column of the data, the wavenumber array, to systematically shift the position of the processed spectra.

---

### Signal-to-Noise Ratio (SNR):

SNR was calculated as specified by **McCreery (2000, Chap 4.)**. Briefly, successive replicates of each compound were subtracted to remove contributions from the Raman band and background features to investigate the contribution of noise to the signal. SNR was calculated about the highest intensity Raman peak (Normalized peak height of 1 before background subtraction).

$$
\text{SNR}=\frac{Y_{avg}}{\left(\sigma_{noise}/\sqrt{2}\right)}
$$

Where $\text{Y}_{avg}$ is an average of the peak height above background of the highest-intensity Raman band across successive replicates. $\sigma_{noise}$ is the average of the standard deviation (STD) of the noise calculated under the footprint of the highest-intensity Raman band from each replicate.  $\sigma_{noise}$  was calculated from a 24 wavenumber range about the peak maximum. Before determination of the SNR, each spectra was normalized in intensity between 0 and 1, and a background subtraction was performed using an asymmetric least squares smoothing algorithm (Eilers & Boelens 2005). 

---

### Signal-to-Background Ratio (SBR):

The SBR is an indication of peak strength relative to the noise about the spectral background. The calculated SBR is a less rigorous approximation of the SNR that can be calculated using a single spectra as opposed to the multiple replicates required for proper SNR calculations (**McCreery 2000, Chap. 4**).
$$
\text{SBR} = \frac{Y}{2\sigma_{background\:noise}}
$$

Where $\text{Y}$ is the height of the tallest Raman peak above the spectral background, and $\sigma_{background\:noise}$ is the standard deviation of noise about the longest stretch of background without any peaks. The spectral background was fit using an asymmetric least squares smoothing algorithm (Eilers & Boelens 2005) and the STD of the background noise was calculated about the flattened background. 

----
### Library Contents

The file: `SampleDetails.csv` includes sample names, calibration parameters, laser power level, sub acquisition count, SNR, and SBR, as well as the International Union of Pure and Applied Chemistry (IUPAC) name, Chemical Abstracts Service (CAS) number, SMILES, and International Chemical Identifier (InChI) key for compounds where it was available. 

Data:
1. Unprocessed Time-Gate Raman Data (`SampleName_3D_Raw.csv`)
	These files have 15 header lines which includes details for calibration. Delineation is by semicolon (;). Line 16 is the time axis in unit nanoseconds. The first data column is the wavenumber axis in units $\textsf{cm}^{-1}$. The data consists of a (1429,100) matrix of intensity values.
	
2. Processed Time-Gate Raman Data (`SampleName_Proc.csv`)
	These files have 4 header lines including sample name and gating information. Delineation is by semicolon (;). The data is presented in 2-column format where column 1 is the wavenumber axis with units $\textsf{cm}^{-1}$ and column 2 is calibrated, normalized intensity (A.U.). The data consists of a (1429,2) array.

### References:

Eilers, P.H.C., Boelens, H.F.M., (2005). Baseline Correction with Asymmetric Least Squares Smoothing. Leiden University Medical Centre report, 1(1), 5.

McCreery, R.L., (2000). Calibration and Validation, in: McCreery, R.L., Raman Spectroscopy for Chemical Analysis. John Wiley & Sons, Inc.

McCreery, R.L., (2000). Signal-To-Noise in Raman Spectroscopy, in: McCreery, R.L., Raman Spectroscopy for Chemical Analysis. John Wiley & Sons, Inc.

##### NIST Disclaimer$^{‡}$: 

Certain commercial equipment, instruments, or materials are identified in this paper in order to adequately specify experimental procedure. Such identification does not imply recommendation or endorsement by the National Institute of Standards and Technology, nor does it imply that the materials or equipment identified are necessarily the best available for the purpose.

