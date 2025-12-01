# TCP ENewReno: Enhancing Network Efficiency in High-Density Networks

![NS-2](https://img.shields.io/badge/Simulator-NS--2-blue)
![Language](https://img.shields.io/badge/Language-C%2B%2B%20%7C%20TCL-orange)
![Domain](https://img.shields.io/badge/Domain-Networking%20%7C%20Congestion%20Control-green)

## 📄 Abstract
**TCP ENewReno** is a novel TCP variant designed to enhance congestion control efficiency in high-density and delay-sensitive network environments (such as 5G). Unlike traditional TCP variants (Reno/NewReno) that rely solely on packet loss or basic heuristics, ENewReno introduces an **adaptive congestion avoidance mechanism**. 

It leverages real-time bandwidth estimation through the **Delay-to-Throughput Ratio (DTR)** to dynamically adjust the Congestion Window (CWND), resulting in higher throughput and fairer bandwidth allocation.

## 🚀 Key Features
* **Adaptive Congestion Control:** Dynamically adjusts CWND based on real-time DTR analysis rather than fixed heuristics.
* **High-Density Optimization:** Tested successfully with 300 User Equipment (UE) nodes in a mixed wired-wireless topology.
* **Improved Fairness:** Achieves a higher Jain’s Fairness Index (JFI) compared to standard TCP variants.
* **NS-2 Integration:** Implemented as a custom agent in the Network Simulator 2 framework.

## ⚙️ Algorithm & Methodology
The core innovation of TCP ENewReno lies in its ability to estimate network capacity using the Delay-to-Throughput Ratio (DTR).

### 1. DTR Calculation
At each acknowledgment (ACK), the DTR is calculated as:
$$DTR = \frac{\text{Estimated RTT}}{\text{Current Throughput}}$$

### 2. CWND Adaptation
The change in DTR ($\Delta DTR$) determines how the Congestion Window (CWND) is adjusted:
$$\Delta DTR = DTR_{current} - DTR_{previous}$$

The control logic applies the following rules based on thresholds ($\beta$):
* **Congestion Detected ($\Delta DTR > \beta$):** * `CWND = CWND * 0.8` (Multiplicative Decrease)
* **Available Bandwidth ($\Delta DTR < -\beta$):** * `CWND = CWND + (CWND / α)` (Additive Increase)
* **Stable State ($|\Delta DTR| \le \beta$):** * `CWND` remains unchanged to prevent oscillation.

## 📊 Performance Results
The protocol was evaluated against TCP Reno and TCP NewReno using NS-2 simulations.

| Metric | TCP Reno | TCP NewReno | **TCP ENewReno** | Improvement |
| :--- | :--- | :--- | :--- | :--- |
| **Throughput (Mbps)** | 3.69 | 3.99 | **5.37** | **~34.5%** |
| **Avg Delay (ms)** | 3.20 | 3.20 | **3.20** | Stable |
| **Fairness (JFI)** | 0.686 | 0.715 | **0.716** | Highest Fairness |
| **Avg CWND** | 4.17 | 2.64 | **4.20** | Optimal Utilization |

> *Simulation conditions: 100 nodes per variant, FTP traffic, 10Mbps link bandwidth.*

## 🛠️ Installation & Usage

### Prerequisites
* **NS-2 (Network Simulator 2)** installed on a Linux environment.
* **Gnuplot** or **Xgraph** for visualization.



## 📈 Analysis
The simulation traces demonstrate that **TCP ENewReno** maintains a larger congestion window without causing bufferbloat, effectively balancing the trade-off between latency and throughput.

*Refer to the `analysis/` folder for generated trace files and throughput graphs.*

## 📚 References
Based on the research paper: *Enhancing Network Efficiency Through TCP E-newreno Congestion Control in High-Density Network*.
1.  Floyd, S., & Henderson, T. (1999). TCP NewReno: Congestion Control (RFC 2582).
2.  Jain, R., et al. (1984). A Quantitative Measure of Fairness.
3.  ns-2 Network Simulator. https://www.isi.edu/nsnam/ns/

---
*Project developed as part of final year Engineering curriculum.*
