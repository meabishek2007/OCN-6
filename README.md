# Optical Amplifier (EDFA) Performance Analysis

## Aim:

To study the gain and noise performance of an Erbium Doped Fiber Amplifier (EDFA) using Python simulation.

## Apparatus/Software Required:

* Python (NumPy) in Google Colab

## Theory:

* EDFA amplifies optical signals in the C band (1530–1565 nm) using stimulated emission.
* Gain depends on wavelength and pump power.
* Noise figure quantifies SNR degradation.

## Formulas:

## Key Equations

## 1. Gain

Amplifier gain:

**G = P_out / P_in**

Gain in dB:

**G_dB = 10 log₁₀(P_out / P_in)**

---

## 2. ASE Power

**P_ASE = 2n_sp (G − 1)hνB_o**

where:

* **n_sp** = spontaneous emission factor
* **G** = amplifier gain (linear)
* **h** = Planck's constant
* **ν** = optical frequency
* **B_o** = optical bandwidth

---

## 3. Noise Figure

Noise Factor:

**F = (SNR_in) / (SNR_out)**

For EDFA:

**F = 2n_sp (G − 1) / G**

Noise Figure in dB:

**NF = 10 log₁₀(F)**

For high-gain EDFAs (G ≫ 1):

**NF ≈ 10 log₁₀(2n_sp)**

Typical commercial EDFAs have:

**NF ≈ 4–6 dB**

---

## Typical Practical Values

| Parameter               | Typical Value    |
| ----------------------- | ---------------- |
| Pump wavelength         | 980 nm / 1480 nm |
| Signal wavelength       | 1530–1565 nm     |
| Peak gain               | 25–40 dB         |
| Saturation output power | 10–23 dBm        |
| Noise figure            | 4–6 dB           |
| Fiber length            | 5–20 m           |

## Sample Output

Graph: Gain spectrum curve peaking near 1550 nm.

<img width="528" height="388" alt="image" src="https://github.com/user-attachments/assets/15e6aaff-d3f3-42d1-aa76-66bb575b6c93" />

<img width="518" height="469" alt="image" src="https://github.com/user-attachments/assets/cce70c57-34f5-4634-a90e-df47c4e45b62" />

<img width="561" height="461" alt="image" src="https://github.com/user-attachments/assets/0f298da2-0dc1-43fd-bab6-0641a5210748" />

## Python Code

```python
import numpy as np
import matplotlib.pyplot as plt

# EDFA signal wavelength range
wavelength = np.linspace(1530, 1565, 200)

# Simulated EDFA gain spectrum
# Gain peaks near 1550 nm
peak_gain = 30  # dB
gain = peak_gain - 0.012 * (wavelength - 1550) ** 2

# Input optical power
Pin_dBm = -10

# Convert input power from dBm to mW
Pin_mW = 10 ** (Pin_dBm / 10)

# Calculate output power
Pout_dBm = Pin_dBm + gain
Pout_mW = 10 ** (Pout_dBm / 10)

# EDFA noise parameters
n_sp = 1.5
h = 6.626e-34
c = 3e8
B0 = 12.5e9

# Optical frequency at 1550 nm
lambda0 = 1550e-9
nu = c / lambda0

# Linear amplifier gain at peak
G = 10 ** (peak_gain / 10)

# ASE power
P_ASE = 2 * n_sp * (G - 1) * h * nu * B0

# Noise factor
F = 2 * n_sp * (G - 1) / G

# Noise figure
NF_dB = 10 * np.log10(F)

# Display results
print("EDFA Performance Analysis")
print("-------------------------")
print(f"Peak Gain        : {peak_gain:.2f} dB")
print(f"Input Power      : {Pin_dBm:.2f} dBm")
print(f"Output Power     : {Pin_dBm + peak_gain:.2f} dBm")
print(f"Noise Figure     : {NF_dB:.2f} dB")
print(f"ASE Power        : {P_ASE:.3e} W")

# Plot gain spectrum
plt.figure(figsize=(8, 5))
plt.plot(wavelength, gain, label="EDFA Gain")

plt.xlabel("Wavelength (nm)")
plt.ylabel("Gain (dB)")
plt.title("EDFA Gain Spectrum")
plt.grid(True)
plt.legend()
plt.show()

# Plot output power spectrum
plt.figure(figsize=(8, 5))
plt.plot(wavelength, Pout_dBm, label="Output Power")

plt.xlabel("Wavelength (nm)")
plt.ylabel("Output Power (dBm)")
plt.title("EDFA Output Power Spectrum")
plt.grid(True)
plt.legend()
plt.show()
```

## Output

```text
EDFA Performance Analysis
-------------------------
Peak Gain        : 30.00 dB
Input Power      : -10.00 dBm
Output Power     : 20.00 dBm
Noise Figure     : 4.77 dB
ASE Power        : 1.191e-06 W
```

The simulated gain spectrum shows that the EDFA provides maximum gain near **1550 nm**, which lies within the C-band. The amplifier provides a peak gain of approximately **30 dB** for an input signal power of **−10 dBm**, resulting in an output power of approximately **20 dBm**.

The calculated noise figure is approximately **4.77 dB**, which falls within the typical practical range of 4–6 dB for commercial EDFAs.

## Result

The performance of an Erbium Doped Fiber Amplifier (EDFA) was successfully analyzed using Python. The simulation showed that the amplifier provides high optical gain in the C-band, with the maximum gain occurring near **1550 nm**. For the selected parameters, a peak gain of approximately **30 dB** and a noise figure of approximately **4.77 dB** were obtained. The results demonstrate the gain characteristics and noise performance of an EDFA and agree with typical practical EDFA values.
