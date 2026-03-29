# High-efficiency, Foundry-compatible Silicon Grating Couplers

**Keywords:** Silicon photonics, Grating coupler, Fibre-to-chip integration

## Abstract
Efficient fibre-to-chip coupling remains a primary bottleneck in silicon photonics. Standard two-dimensional (2D) grating optimizations often fail when translated to three-dimensional (3D) layouts, suffering from severe spectral degradation due to non-ideal diffraction and parasitic Fabry-Perot interference. 

In this work, the author proposes a single-etch 3D grating coupler design that systematically resolves these problems. By combining a focusing geometry with an apodized grating profile, we reshape the coupling strength and redirect the diffracted wavefront to suppress multi-path reflections. This work provides a straightforward, tape-out-ready methodology for realizing high-efficiency, spectrally stable optical interfaces without complex reflectors.

## ⚠️ Important Usage Note
**This repository contains only `.lsf` scripts and does not include the pre-calculated simulation results.** 

* **Software Version:** All scripts and simulation environments are configured and verified for **Ansys Lumerical FDTD 2025R2**.
* **Execution:** You may observe that the results from the first run differ slightly from those reported in the paper. It is highly recommended to run the simulations 2 to 3 times, after which the results will successfully recover to the exact values presented in the paper.

## ⚙️ Physical Model and Parameter Settings
Full-wave electromagnetic simulations of the proposed grating couplers were conducted using both 2D and 3D finite-difference time-domain (FDTD) solvers. The physical model and fundamental simulation environment were configured using the following parameters:

* **Platform Architecture:** Standard foundry-compatible SOI platform comprising a **220-nm silicon device layer**, a **2 μm buried oxide (BOX) layer**, and an **oxide top cladding**.
* **Materials:** Silicon (Si) and silicon dioxide (SiO₂) material properties were described by the **Palik dispersion models**, providing accurate refractive-index data across the target 1550 nm telecommunication band.
* **Etch Depth ($e_d$):** A single **80-nm** shallow etch.
* **Output Waveguide:** A **500 nm-wide** single-mode silicon waveguide.
* **Grating Parameters (Final 3D Focusing Design):** Consists of **16 curved grating teeth**, with the period chirped from **0.635 to 0.675 μm** and the fill factor chirped from **0.72 to 0.41**.
* **Excitation Source:** A TE-polarized **Gaussian beam source** (waist radius **5.2 μm**, incidence angle **20°**) was launched to emulate fiber excitation.
* **Boundary Conditions:** All peripheral boundaries of the computational domain were terminated with **perfectly matched layers (PML)** to absorb outgoing radiation and eliminate artificial reflections.
* **Meshing:** A non-uniform conformal meshing scheme was adopted. In the grating coupling region, localized mesh override regions were applied with refined cell sizes of **Δx, Δy, Δz ≤ 10-20 nm**.
* **Monitors:** Coupling efficiency into the fundamental TE mode was extracted directly from **mode-expansion monitors** placed at the waveguide output port, with supporting **power transmission monitors** used to verify field profiles and energy conservation.

## 📊 Results
The simulation codes are divided into three stages to demonstrate the failure of direct 2D-to-3D translation and the recovery of performance via wavefront engineering:

### 1. 2D Optimized Straight Grating Coupler
To establish a robust design, the longitudinal coupling mechanics were first isolated using a 2D model. 
* **Performance:** The optimized 2D straight grating exhibits a peak transmission of **0.692** at 1550 nm (coupling loss of approx. -1.60 dB). The extracted 3 dB bandwidth is 54.19 nm.
* **Characteristics:** The spectrum is smooth and follows a near-ideal sinc² envelope. The incident Gaussian beam is diffracted efficiently into the grating region and then transferred into the guided mode with relatively weak parasitic standing-wave features.

<img width="1815" height="745" alt="2D" src="https://github.com/user-attachments/assets/c8a79364-b0e8-45f9-8353-51cc0aff58dc" />
> **Figure 1.** 2D optimized straight grating coupler. **a)** Simulated transmission spectrum. **b)** Electric-field distribution showing efficient diffraction and smooth coupling.

### 2. Performance Degradation in the 3D Straight-Grating Coupler
When the same straight-grating design is evaluated in 3D, its performance degrades significantly due to neglected multi-path reflections at the device boundaries.
* **Performance:** The peak transmission drops to **0.405** (-3.92 dB), and the maximum shifts from 1550 nm to approximately 1560 nm. 
* **Characteristics:** The spectral profile is no longer smooth: pronounced oscillations appear across the passband. The 3D straight grating exhibits chaotic interference fringes in the surrounding area, consistent with Fabry-Perot oscillations caused by reflection and multi-path re-interference.

<img width="1745" height="757" alt="3D 1" src="https://github.com/user-attachments/assets/c802dce9-2868-45ef-89ef-4f3f62510031" />
> **Figure 2.** 3D straight-grating coupler. **a)** Simulated transmission spectrum showing a reduced peak transmission and a red-shifted maximum. **b)** Electric-field distribution showing strong superposed interference fringes.

### 3. Recovery by the 3D Focusing-Apodized Grating Coupler
To address this limitation, the straight grating was redesigned as a 3D focusing-apodized grating coupler. The grating trenches were mapped onto confocal ellipses to direct the diffracted field into a submicron waveguide.

* **Performance:** The optimized 3D focusing-apodized grating substantially restores the desired device behavior. The peak transmission increases to **0.555 (–2.56 dB)** precisely at 1550 nm, while the 3 dB bandwidth broadens to **61.05 nm**.
* **Characteristics:** The oscillatory modulation is strongly suppressed. The interference pattern is much cleaner and the radiated field is more spatially organized.

<img width="1753" height="772" alt="3D 2" src="https://github.com/user-attachments/assets/abea5816-604b-4c0d-8fc8-05efee73b9ba" />
> **Figure 3.** Simulation result of optimized 3D focusing-apodized grating coupler. **a)** Simulated transmission spectrum. **b)** Electric-field distribution showing clean focusing into the taper entrance and reduced parasitic interference.

## 💡 Discussion and Conclusion

We systematically bridged the gap between idealized 2D designs and realistic 3D physical behaviors in silicon grating couplers. The performance limitations commonly observed in single-etch SOI grating couplers largely come from uncontrolled 3D parasitic interference and lateral mode mismatch. 

These effects are successfully reduced through the combined use of focusing and apodization:
1. **Focusing geometry:** Reshapes the diffracted wavefront, suppressing divergence and reducing leakage to improve mode overlap with the fiber.
2. **Apodization (chirped fill factor):** Gradually modifies the effective index and scattering strength along the propagation direction, effectively breaking the parasitic effects and suppressing coherent back-reflections.

Without relying on exotic reflectors or complex multi-etch processes, the optimized device achieves a simulated peak transmission of 0.555 (–2.56 dB) accurately targeted at 1550 nm, alongside a broad 3-dB bandwidth of 61.05 nm and a remarkably smooth spectral envelope. This approach demonstrates that wavefront engineering may unlock high-performance, spectrally stable optical I/O interfaces fully compatible with standard 220-nm SOI foundries.
