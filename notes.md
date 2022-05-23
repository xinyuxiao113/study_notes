# 2022.05.15
## Use GPU

Nvidia command introduction:
https://medium.com/analytics-vidhya/crux-of-gpu-28fe7d37dd28

1. Monitors your GPU. Understand about this utility in detail in explained output of nvidia-smi.
```
$ nvidia-smi
```
2. This tool is similar like above except for the information displayed in detail.
```
$ nvidia-smi –a
```
3. It monitors your GPU every second, refreshing and tracking the output itself for each second.
```
$ watch –n 1 nvidia-smi
```
4. This tool tracks the memory usage of your GPUs while running the model, for every second.
```
$ watch –n 1 free –m
```

# 2022.05.16
## split training
split data: 
$$
data.y:[batch, N_s, N_{pol}] \rightarrow [batch, ] \\
data.x:[batch, N_{symb}, N_{pol}]
$$

idea:
- sequence embedding
- auxiliary features + dynamics
- Graph diffusion

# 2022.0517
New problem:
---
1.超大带宽下的NLSE高精度模拟问题 @Remi

New idea:
---
1. XPM noise statistical model + Adaptive filter.
2. 对比用Adaptive filter 和 NNDBP 解决XPM noise

# 2022.0518
coding
---



preparing report
---
1. paper: 2022_XPM_LDP.
2. paper: 2014_ESSFM.
3. paper: 2014_multi-channel DBP.
4. NLSE deriviation.

**Linear step:**
$$
u_{k+\frac{1}{2}}(t) = \mathcal{F}^{-1}(\mathcal{F}(u_k(t)) \cdot \exp(j\frac{\beta_2 \Delta z}{2} \omega^2))
$$
$$
v_{k+\frac{1}{2}}(t) = \mathcal{F}^{-1}(\mathcal{F}(v_k(t)) \cdot \exp(j\frac{\beta_2 \Delta z}{2} \omega^2))
$$

**Nonlinear step:**
$$
u_{k+1}(t) = u_k(t) \exp\left(j\gamma \Delta z_{eff} (|u_{k+\frac{1}{2}}(t)|^2 + 2|v_{k+\frac{1}{2}}(t)|^2)\right)
$$

$$
v_{k+1}(t) = v_k(t) \exp\left(j\gamma \Delta z_{eff} (|v_{k+\frac{1}{2}}(t)|^2 + 2|u_{k+\frac{1}{2}}(t)|^2)\right)
$$

Meta:
---
**Linear step:**
$$
u_{k+\frac{1}{2}}(t) = \mathcal{F}^{-1}(\mathcal{F}(u_k(t)) \cdot \phi_{\theta}(u_k(t)))
$$

**Nonlinear step:**
$$
u_{k+1}(t) = u_k(t) \exp\left(j\gamma \Delta z_{eff} (|u_{k+\frac{1}{2}}(t)|^2 + \psi_{\mu}(u_{k+\frac{1}{2}}(t)))\right)
$$

# 2022.05.22
---
optical simulation parameters:
### 光纤参数
| 参数 | 数值 | 单位 |
| ----    | ----------- |----|
| span length | 75 | km |
| span numbers | 15 |  | 
| attenuation $\alpha$ |  0.2 | dB/km |
| Chromatic dispersion parameter $D$ | 16.5 | ps/nm/km |
| nonlinear parameter $\gamma$| 1.3 |  1/W/km|
| EDFA noise figure | 4.5  | dB |

### 发射机参数
| 参数 | 数值 | 单位 |
| ----    | ----------- |----|
| number of channels | 25 |  |
| number of bits| 4e6 |  | 
| modulation format | 16QAM | |
| pulse shape | raised cosine | |
| roll off | 0.1 ||
| Power    | 0    | dBm |
| symbol rate | 36 | Gbaud |
| central wave length | 1550 | nm|
| polarization modes | 2| |

### 接收机参数
| 参数 | 数值 | 单位 |
| ----    | ----------- |----|
| linewidth | 100 | kHz |
| frequency offset  | [-1,1] | GHz |