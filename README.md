# TGRS-Plasticizer-Library
This library consists of time gated Raman spectra of 91 plasticizers included in the Scientific Polymer Products Inc. Plasticizer Kit‡. The sample list can be found in the file: SampleDetails.csv. Plasticizers were measured at least in duplicate. Data was collected on a PicoRaman spectrometer (Timegate Instruments) using a 532 nm pulsed laser. The spectrometer was coupled through a fiber-optic probe. The wavenumber range of the measurements were calibrated using a polystyrene reference sample (PSRS) comparing the locations of 4 primary peaks, [620.9, 1001.4, 1031.8, 1602.3] (McCreery 2000, Chap. 10). Liquid samples were measured in aluminum sample pans, and solid samples were compacted using a pellet press. Sampling conditions were selected to minimize measured fluorescence and accompanying noise in the time gated window. Parameters of Laser Power (mW) and collection time (s) were selected to achieve a Signal-to-Noise Ratio (SNR) exceeding 100. Collection times are reported in seconds and the Timegate software metric of Sub Acquisitions (SA) where samples were collected using 100 SA (13 seconds) or 300 SA (39 seconds). Some samples had significant fluorescence interference after time-gating and could not achieve an SNR >100. These samples are included in the library as is.
Specific information regarding the sampling conditions for each plasticizer are included in the file: SampleDetails.csv.

----

Data Calibration:

During the data collection period, the instrument required repairs resulting in a change in the wavenumber set point of the detector and requiring different shift factors to calibrate the data, as documented in SampleDetails.csv. The unprocessed files (SampleName_Raw.csv) have not been adjusted with the PSRS calibration. 
The header lines of the unprocessed files include the peak locations of the polystyrene reference sample that was measured during the same data collection session as the present sample and a calibration shift factor calculated using the method detailed below. The calibration shift is already incorporated in the processed data files (SampleName_Proc.csv).

The calibration shift factor represents a weighted average of the deviation between the peak locations of the measured PSRS and standardized PS peak locations reported in McCreery 2000 Chap. 10. Four peaks were assessed because the as-measured peaks presented some variation in their shifted position relative to the standardized peak locations.

Standardized_Peak_location = [620.9, 1001.4, 1031.8, 1602.3] 
Peak_Weighting = [16, 100, 27, 28]  # Where the peak weights correspond to the relative intensity of the respective peaks

As-measured PSRS peaks were compared to the standardized peak locations and the difference in position was recorded. Then a weighted average of the differences was taken using the standardized relative peak intensities reported in McCreery 2000 as weights. To calibrate the data, the calibration shift factor is scalar-added to the wavenumber array to systematically shift the position of the spectra.


Signal-to-Noise Ratio (SNR):

SNR was calculated as specified by McCreery (2000, Chap 4.). Briefly, two successive replicates of each compound were subtracted to remove contributions from the Raman band and background features, isolating the noise. SNR was calculated about the highest intensity Raman peak (Normalized peak height of 1 before background subtraction).

SNR = y_average/ (σ_Noise/sqrt(2))

Where y_average is an average of the peak height of the highest-intensity Raman band between successive replicates after background subtraction. σ_Noise is the standard deviation of the noise under the footprint of the highest-intensity Raman band calculated in a 24 wavenumber range about the peak maximum. σ_Noise was determined as the standard deviation of the magnitude of noise about the spectra of isolated noise relative to an asymmetric least squares fitted background (Eilers & Boelens 2005). Due to many of the compounds in this library being liquids, SNR was calculated using a truncated wavenumber range (400-2500 cm-1 Raman shift) to cut out the Rayleigh-wing (Nielsen 1993) which often yielded the highest signal intensity when present.


Signal-to-Background Ratio (SBR):

The SBR is an indication of peak strength relative to the noise about the spectral background. The calculated SBR is a less rigorous approximation of the SNR that can be calculated using a single spectra as opposed to the multiple replicates required for proper SNR calculations (McCreery 2000, Chap. 4).

SBR = y / (2*σ_Background_Noise)

Where y is the height of the tallest Raman peak above the spectral background, and σ_Background_Noise is the standard deviation of noise about the longest stretch of background without any peaks. The spectral background was fit using an asymmetric least squares smoothing algorithm (Eilers & Boelens 2005) and the average magnitude of the background noise was calculated about the flattened background.

----
The file: SampleDetails.csv includes sample names, calibration parameters, Laser power level, Sub acquisition count, SNR, and SBR, as well as the International Union of Pure and Applied Chemistry (IUPAC) name, Chemical Abstracts Service (CAS) number, and International Chemical Identifier (InChI) key for compounds where it was available. 

Data:
1. Unprocessed Time-Gate Raman Data (SampleName_3D_Raw.csv)
	These files have 15 header lines which includes details for calibration. Delineation is by semicolon (;). Line 16 is the time axis in unit nanoseconds. The first data column is the wavenumber axis in units cm-1. The data consists of a (1429,100) matrix of intensity values.
	
2. Processed Time-Gate Raman Data (SampleName_Proc.csv)
	These files have 4 header lines including sample name and gating information. Delineation is by semicolon (;). The data is presented in 2-column format where column 1 is the wavenumber axis (cm-1) and column 2 is calibrated, normalized intensity (A.U.).


NIST Disclaimer‡: 
	Certain commercial equipment, instruments, or materials are identified in this paper in order to adequately specify experimental procedure. Such 	identification does not imply recommendation or endorsement by the National Institute of Standards and Technology, nor does it imply that the 	materials or equipment identified are necessarily the best available for the purpose.

References:

McCreery, R.L., (2000). Calibration and Validation, in: McCreery, R.L., Raman Spectroscopy for Chemical Analysis. John Wiley & Sons, Inc.

McCreery, R.L., (2000). Signal-To-Noise in Raman Spectroscopy, in: McCreery, R.L., Raman Spectroscopy for Chemical Analysis. John Wiley & Sons, Inc.

Eilers, P.H.C., Boelens, H.F.M., (2005). Baseline Correction with Asymmetric Least Squares Smoothing. Leiden University Medical Centre report, 1(1), 5.

Nielsen, O.F., (1993). Low-Frequency Spetroscopic Studies of Interactions in Liquids. Annual Reports Section "C"(Physical Chemistry), 90, 3-44.
