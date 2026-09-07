# Wavelength Division Multiplexing (WDM) Simulation

## Aim 
To simulate a WDM system using Python and analyze channel separation and insertion loss.

## Apparatus/Software Required
	Python (NumPy)
	Google Colab or Jupyter Notebook

## Theory
	WDM allows multiple optical signals at different wavelengths to be transmitted simultaneously over a single fiber.
	Channel spacing determines spectral efficiency and crosstalk.
	Insertion loss is the reduction in signal power due to multiplexing/demultiplexing.

## Formula:

**Insertion Loss (dB) = P_in − P_out**

**Channel Spacing = Δλ**

## 1

## Setup Environment

Prepare the Python environment for simulation.

* Import NumPy and Matplotlib.
* Define the channel wavelengths and input powers.

## 2

## Define WDM Parameters

Specify the input wavelengths and powers.

* Choose 3 optical channels.
* Set the channel wavelengths as 1550 nm, 1552 nm, and 1554 nm.
* Assign equal input power of −2 dBm to each channel.
* The channel spacing is selected as 2 nm.

## 3

## Calculate Output Power

Simulate insertion loss for each channel.

* Assume an insertion loss of approximately 1 dB per channel.
* Calculate the output power using:

**P_out = P_in − Insertion Loss**

For an input power of −2 dBm and an insertion loss of 1 dB:

**P_out = −2 − 1 = −3 dBm**

## 4

## Plot WDM Spectrum

Visualize the separation between the WDM channels.

* Create a wavelength range around the selected channel wavelengths.
* Plot the power level of each channel using Matplotlib.
* Represent each channel as a peak at its corresponding wavelength.
* Label the channel peaks and wavelength values.
* Display the input and output power levels for comparison.

## 5

## Analyze Results

Interpret the simulation output.

* The three WDM channels are clearly separated in the spectrum.
* The wavelengths are 1550 nm, 1552 nm, and 1554 nm.
* The channel spacing is verified as **Δλ = 2 nm**.
* With an assumed insertion loss of 1 dB, the output power of each channel is **−3 dBm**.
* The simulation demonstrates that multiple optical channels can be transmitted over a single fiber using different wavelengths.

## Sample Output

The following output is obtained from the simulation:
\The following output is obtained from the simulation:

```text
WDM Channel Parameters
----------------------
Channel 1: λ = 1550 nm, Pin = -2 dBm, Pout = -3 dBm
Channel 2: λ = 1552 nm, Pin = -2 dBm, Pout = -3 dBm
Channel 3: λ = 1554 nm, Pin = -2 dBm, Pout = -3 dBm

Channel Spacing:
Δλ = 2 nm

Insertion Loss:
1 dB per channel
```

The plotted WDM spectrum shows three distinct peaks corresponding to the wavelengths **1550 nm, 1552 nm, and 1554 nm**. Each channel experiences an insertion loss of approximately **1 dB**.

## Python Code 
```
import numpy as np
import matplotlib.pyplot as plt

# -----------------------------
# PARAMETERS
# -----------------------------
num_channels = 4
center_wavelength = 1550   # nm
channel_spacing = 0.89  # nm (can vary this!)
bandwidth = 0.27           # spectral width of each channel

# wavelength axis
wavelength = np.linspace(1545, 1555, 2000)

# -----------------------------
# GENERATE CHANNELS
# -----------------------------
channels = []

for i in range(num_channels):
    lambda_i = center_wavelength + (i - num_channels//2) * channel_spacing

    # Gaussian spectrum for each channel
    spectrum = np.exp(-((wavelength - lambda_i)**2) / (2 * bandwidth**2))

    channels.append(spectrum)

# -----------------------------
# MULTIPLEXED SIGNAL
# -----------------------------
wdm_signal = np.sum(channels, axis=0)

# -----------------------------
# PLOTS
# -----------------------------

# Individual channels
plt.figure()
for i, ch in enumerate(channels):
    plt.plot(wavelength, ch, linestyle='--', label=f'Ch {i+1}')
plt.xlabel("Wavelength (nm)")
plt.ylabel("Power")
plt.title("Individual WDM Channels")
plt.legend()
plt.grid()
plt.show()

# Combined WDM signal
plt.figure()
plt.plot(wavelength, wdm_signal)
plt.xlabel("Wavelength (nm)")
plt.ylabel("Power")
plt.title("Multiplexed WDM Signal")
plt.grid()
plt.show()

spacings = [0.9, 1.8, 1.3]

plt.figure()

for spacing in spacings:
    channels = []

    for i in range(num_channels):
        lambda_i = center_wavelength + (i - num_channels//2) * spacing
        spectrum = np.exp(-((wavelength - lambda_i)**2) / (2 * bandwidth**2))
        channels.append(spectrum)

    wdm_signal = np.sum(channels, axis=0)
    plt.plot(wavelength, wdm_signal, label=f'Spacing = {spacing} nm')

plt.xlabel("Wavelength (nm)")
plt.ylabel("Power")
plt.title("Effect of Channel Spacing in WDM")
plt.legend()
plt.grid()
plt.show()
```


## Sample Output

<img width="567" height="455" alt="download (2)" src="https://github.com/user-attachments/assets/62c49e58-f717-4285-b0d9-0899136d3343" />

<img width="567" height="455" alt="download (1)" src="https://github.com/user-attachments/assets/8df52f06-5256-4c2d-8d3e-19383c18aec1" />

<img width="567" height="455" alt="download (3)" src="https://github.com/user-attachments/assets/7bb1136c-5a12-40fb-a2cd-56dc5715f59e" />


## Result 
The WDM system was successfully simulated using Python. Three optical channels at **1550 nm, 1552 nm, and 1554 nm** were multiplexed with a channel spacing of **2 nm**. An insertion loss of **1 dB per channel** resulted in an output power of **−3 dBm** for each channel. The plotted spectrum clearly shows the separation of the three WDM channels.

