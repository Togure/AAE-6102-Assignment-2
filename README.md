# Task 1 
GenAI: Deepseek

link: [https://github.com/Togure/AAE-6102-Assignment-2/edit/main/deepseek-Task1.png](https://github.com/Togure/AAE-6102-Assignment-2/blob/main/deepseek-Task1.png)

## 1.1 Introduction
Global Navigation Satellite Systems (GNSS) have evolved to support increasingly sophisticated smartphone navigation applications, each with distinct accuracy and operational requirements. Consumer-grade applications such as mapping and ride-hailing services typically demand meter-level accuracy, while advanced implementations including augmented reality and autonomous navigation systems require decimeter-to-centimeter precision. Furthermore, applications operating in remote environments necessitate global coverage without dependence on local infrastructure. This analysis examines four principal correction methodologies: Differential GNSS (DGNSS) for local-area corrections, Real-Time Kinematic (RTK) for high-precision positioning, Precise Point Positioning (PPP) for global precise solutions, and the hybrid PPP-RTK approach. Each technique is evaluated across critical parameters including accuracy, coverage, convergence characteristics, and implementation requirements.

##  1.2 Different Methods Comparison
### 1.2.1 Differential GNSS (DGNSS) [1]

#### Technical Principle
DGNSS operates by comparing GNSS measurements between reference stations at known locations and mobile receivers, calculating differential corrections for common errors including atmospheric delays and satellite clock inaccuracies. These corrections are subsequently transmitted to mobile devices for real-time position refinement.

#### Advantages
DGNSS offers significant improvements over standalone GNSS, enhancing typical positioning accuracy from 5-10 meters to 1-3 meters. The system leverages existing ground-based reference station networks, minimizing additional infrastructure requirements while maintaining cost-effectiveness for end-user implementation. Its real-time operation provides immediate corrections without substantial processing delays, making it particularly suitable for dynamic navigation applications.

#### Limitations
The effectiveness of DGNSS is constrained by its dependence on proximity to reference stations, with optimal performance typically limited to within 100 kilometers of correction sources. Urban environments present particular challenges due to signal multipath effects that can substantially degrade accuracy. While the system provides marked improvement over basic GNSS, its precision remains insufficient for applications requiring sub-meter accuracy. Performance consistently degrades with increasing distance from reference stations, limiting its utility in remote or infrastructure-sparse regions.

### 1.2.2 Real-Time Kinematic (RTK) [2]

#### Technical Principle
RTK positioning employs carrier-phase measurements from both reference stations and mobile receivers, resolving integer ambiguities in the carrier-phase data to achieve centimeter-level accuracy. This technique represents the gold standard for high-precision real-time positioning.

#### Advantages
RTK delivers exceptional positioning accuracy in the range of 1-5 centimeters under ideal conditions, making it indispensable for precision applications. The system achieves full operational accuracy immediately after successful initialization and maintains this precision for moving platforms. RTK implementations typically include real-time quality indicators that provide valuable feedback on solution integrity and reliability.

#### Limitations
The performance of RTK is heavily dependent on dense networks of reference stations, typically requiring station spacing of less than 20 kilometers. This infrastructure dependence limits its applicability in regions without adequate station coverage. The technique demands substantial processing power, resulting in significant battery consumption on mobile devices. Signal obstructions in urban canyons or dense foliage can severely degrade performance, and the system requires successful ambiguity resolution during initialization to achieve optimal accuracy.

### 1.2.3 Precise Point Positioning (PPP) [3]

#### Technical Principle
PPP utilizes precise satellite orbit and clock products combined with dual-frequency measurements to achieve precise positioning without local reference stations. The technique incorporates advanced error modeling to mitigate atmospheric and other GNSS error sources across wide areas.

#### Advantages
PPP's most significant advantage lies in its global coverage capability, operating independently of local infrastructure requirements. The system provides decimeter-level accuracy (10-30 centimeters) after convergence and incorporates sophisticated atmospheric and satellite error corrections. This makes PPP particularly valuable for applications in remote regions or maritime environments where local reference stations are unavailable.

#### Limitations
The primary constraint of PPP is its extended convergence time, typically requiring 20-40 minutes to achieve optimal accuracy. The system's performance depends on timely delivery of satellite correction products, introducing latency considerations. Continuous internet connectivity is necessary for correction updates, and the technique demonstrates suboptimal performance for rapidly moving platforms during the convergence period. These characteristics limit PPP's suitability for real-time dynamic applications.

### 1.2.4 PPP-RTK [4]

#### Technical Principle
PPP-RTK represents an innovative hybrid approach that combines elements of PPP and RTK, utilizing both precise satellite products and regional atmospheric corrections. This synthesis enables faster convergence while maintaining wide-area coverage capabilities.

#### Advantages
PPP-RTK achieves centimeter-level accuracy within 1-2 minutes, significantly faster than traditional PPP. The system maintains performance over regional or continental scales and delivers consistent 2-10 centimeter positioning accuracy. Its robust design tolerates moderate signal interruptions, making it more resilient than conventional RTK in challenging environments.

#### Limitations
As an emerging technology, PPP-RTK currently faces limitations in mass-market implementation. The system's complexity stems from its requirement to integrate multiple correction sources, and it demands higher bandwidth for correction data transmission. Presently, only advanced GNSS chipsets support PPP-RTK functionality, though this limitation is expected to diminish as the technology matures.

### 1.2.5 Performance Comparison

| Technique | Accuracy Range | Coverage Radius | Convergence Time | Update Rate | Infrastructure Requirements |
|-----------|----------------|-----------------|------------------|-------------|-----------------------------|
| DGNSS     | 1-3 meters     | <100 km         | Immediate        | 1-10 Hz     | Local reference stations    |
| RTK       | 1-5 cm         | <20 km          | Immediate*       | 1-20 Hz     | Dense station network       |
| PPP       | 10-30 cm       | Global          | 20-40 minutes    | 0.1-1 Hz    | Internet connectivity       |
| PPP-RTK   | 2-10 cm        | Regional/Global | 1-2 minutes      | 1-5 Hz      | Regional correction networks|

*\*After successful initialization*

## 1.3 Application Recommendations

For urban navigation applications where meter-level accuracy suffices, DGNSS remains the most practical and cost-effective solution. High-precision applications such as surveying or augmented reality should employ RTK where supporting infrastructure exists. PPP provides the optimal solution for remote operations without local reference stations, particularly in maritime or wilderness environments. Looking forward, PPP-RTK emerges as the most promising technology for ubiquitous high-precision positioning, though its widespread adoption awaits further technological development and infrastructure deployment.

## 1.4 Conclusion
The selection of an appropriate GNSS correction methodology requires careful consideration of accuracy requirements, coverage needs, and available infrastructure. While DGNSS adequately serves most consumer navigation applications, specialized implementations demand more advanced solutions. RTK remains unmatched for precision but carries significant infrastructure requirements, while PPP offers global coverage at the cost of extended convergence times. PPP-RTK represents a compelling middle ground that balances accuracy, coverage, and convergence characteristics, positioning it as the likely future standard for smartphone navigation as supporting technologies mature. Continued advancements in GNSS chipset capabilities and correction service availability will be crucial in realizing this potential.



# Task 2
The skymask is a 361*2 matrix, containing the azimuth angle and elevation angle of the building silhouette in the skymask. In the collected urban dataset (90S), the satellite's azimuth and elevation can be considered relatively static (movement less than 1°). Therefore, each satellite's visibility can be distinguished directly, as shown in Fig.1.1. The red dot is the NLOS satellite, and the blue dot is the LOS satellite.

![Fig.1.1 The skyplot with skymask.](https://github.com/Togure/AAE-6102-Assignment-2/blob/main/skyplot.jpg)  

Based on the visibility of different satellites, we can give more weight to the signal obtained from the LOS satellite in WLS. However in the urban dataset, our SDR can only track 4 satellites. 4 observations and 4 variables result in only one solution. Therefore, based on our SDR system in Assignment 1, using skymask will not acquire obvious gains compared to the original LS. 

 ![Fig.1.2 Positioning result of urban dataset.](https://github.com/Togure/GNSS-SDR/blob/main/figues/4.2.jpg)  
 
Fig.1.2 is the result of urban. (a) shows the estimated velocity result. (b) is the positioning error. (c) is the positioning plot and sky-plot.
(d) is the CDF of the positioning error of LS and WLS. 

Of course, if a more optimized SDR algorithm is used,, interference may be suppressed and more satellites may be tracked. In this way, the skymask-based satellite weight positioning method can achieve higher positioning accuracy.
# Task 3
GenAI: Deepseek

To implement RAIM, we follow these steps:

## 3.1 Calculate Test Statistics
In the leastsquarepos.m, the step to calculate residual $Y$ is 
```matlab
   omc(i) = ( obs(i) - norm(Rot_X - pos(1:3), 'fro') - pos(4) - trop ); 
```

the residual of WLS and LS method are as follows, within 8 meters totally.
![Fig.1.3 The residual of WLS and LS of open-sky dataset.](https://github.com/Togure/AAE-6102-Assignment-2/blob/main/residual.jpg)  

then we calculate test statistics (WSSE) and T_{threshold} based on

$WSSE = \sqrt{Y^TW(I-P)Y}$

and

$T(N,P_{FA}) = \sqrt{Q_{\chi^2,N-4}(1-P_{FA})}$

where Qχ2,N−4(·) stands for the quantile function of Chi-square distribution with degree of freedom of N − 4. 
```
   WSSE_sqrt = sqrt(y'*W*(I-P)*y);
```
```
   P_fa = 1e-2;
   sigma = 3;
   n_sat = 5; % number of tracked satelite 
   dof = n_sat - 4;
   T_threshold = sqrt(chi2inv(1 - P_fa, dof));
```
![Fig.1.4 Test statistics and T threshold.](https://github.com/Togure/AAE-6102-Assignment-2/blob/main/SSE.jpg)  

## 3.2 Define 3D protection level (PL)


TO calculate the  3D protection level, first, we should calculate the SLOPE:

$SLOPE = \frac{\sqrt{S_{xi}^2+S_{yi}^2+S_{zi}^2}}{\sqrt{W_{ii}*(1-P_(ii))}}$

and the PL:

$PL = \max \{SLOPE\}*T_{threshold}(N,P_{FA})  + k(P_{MD}) * \sigma $

where σ = 3m, and k(PMD) = QN(1 − PMD/2) where QN(·) is the quantile function of standard normal distribution [5].

```
   Pslope(i) = sqrt(sum((K(1:3,i)).^2)) * sqrt(1/W(i,i)) / sqrt(1-P(i,i));
   PL = max(Pslope) * Detect_results.Thres + norminv(1-P_md/2) * URA;
```
## 3.3 Standford Chart

![Fig.1.5 Standford Chart of the RAIM system.](https://github.com/Togure/AAE-6102-Assignment-2/blob/main/standford.jpg)  


# Task 4
GenAI: Deepseek

link: [https://github.com/Togure/AAE-6102-Assignment-2/edit/main/deepseek-Task4.png](https://github.com/Togure/AAE-6102-Assignment-2/blob/main/deepseek-Task4.png)
# Unique Challenges of Low Earth Orbit Satellite Navigation Systems

## 4.1 Introduction

Low Earth Orbit (LEO) satellite constellations have emerged as a potential augmentation to traditional Global Navigation Satellite Systems (GNSS), offering several distinct advantages. Operating at altitudes between 500-2,000 km, LEO systems exhibit significantly lower signal latency (20-30 ms) compared to Medium Earth Orbit (MEO) systems like GPS (120 ms). The closer proximity to Earth enables received signal strengths 10-100 times greater than conventional GNSS, particularly beneficial for urban canyon and indoor positioning scenarios. Furthermore, the rapid orbital motion of LEO satellites provides faster geometric diversity, enhancing positioning robustness against obstructions and interference [6].

However, these advantages come with substantial technical challenges. The high orbital velocity induces severe Doppler effects, while the limited coverage area of individual satellites necessitates large constellation sizes. Additionally, the dynamic LEO environment subjects satellites to pronounced atmospheric drag and gravitational perturbations, requiring frequent orbit determination updates. This paper systematically examines these challenges through current and proposed LEO navigation systems, including Iridium's operational STL service, SpaceX's experimental Starlink utilization, Xona's dedicated Pulsar constellation, and China's planned Hunyuan system. The analysis concludes with recommended mitigation strategies for future LEO navigation implementations [7].

## 4.2 Fundamental Technical Challenges

### Signal Dynamics and Processing Requirements

The orbital velocity of 7.8 km/s at 550 km altitude creates extreme Doppler shifts exceeding ±30 kHz, compared to the ±5 kHz typical of MEO GNSS. This imposes stringent requirements on receiver signal processing architectures. Modern LEO navigation receivers must implement carrier tracking loops with update rates exceeding 100 Hz, compared to 10-20 Hz for GNSS receivers. The rapid signal dynamics also necessitate advanced cycle slip detection algorithms capable of identifying and correcting phase discontinuities within single-second intervals. These processing demands increase receiver power consumption by 30-50% compared to conventional GNSS solutions.

### Visibility and Coverage Constraints

The limited coverage characteristics of LEO satellites present significant system design challenges. A single LEO satellite at 550 km altitude provides approximately 5,000 km² of coverage, compared to 140,000 km² for a MEO satellite at 20,200 km. This reduced coverage area, combined with visibility durations of only 15-20 minutes per pass, creates complex system architecture requirements. To maintain continuous dual-coverage globally, constellations must deploy at least 200 satellites in carefully optimized orbital planes. The resulting handover frequency between satellites demands robust network synchronization and timing transfer mechanisms to prevent positioning discontinuities.

## 4.3 System-Specific Analysis

### Iridium STL Service

The Iridium constellation represents the first operational LEO navigation augmentation system, leveraging its existing 66-satellite communications network at 780 km altitude. The Satellite Time and Location (STL) service provides positioning accuracy of 7.8 meters (95% horizontal) through time-difference measurements of L-band burst signals. However, the system exhibits several limitations: the lack of carrier-phase observations prevents high-accuracy positioning, and the inclined orbital planes create coverage gaps near the equator. Recent upgrades have improved time transfer accuracy to <50 ns UTC alignment, demonstrating the potential for LEO-based timing services.

## 4.4 Comparative Assessment

### Accuracy Performance Metrics

Current LEO navigation systems exhibit varying levels of positioning performance. Iridium's STL service achieves 2.5 meters pseudorange precision (1σ) but lacks carrier-phase capability. Experimental Starlink navigation demonstrates 5.8 meters pseudorange accuracy with centimeter-level carrier-phase potential, though requiring substantial signal processing. Xona's Pulsar system, designed specifically for navigation, targets 0.3 meters pseudorange and 2 mm carrier-phase precision, comparable to high-end GNSS receivers. These performance differences primarily stem from signal structure design and constellation geometry stability.

## 4.5. Mitigation Strategies

### Advanced Signal Processing Techniques

Modern receiver designs must incorporate several key innovations to address LEO signal challenges. Adaptive Kalman filtering techniques can effectively track the dynamic signal parameters, with state vectors expanded to include higher-order Doppler derivatives. Parallel correlation channel architectures, implementing at least eight simultaneous tracking channels per frequency, maintain lock during rapid signal transitions. Machine learning approaches show particular promise for predicting signal dynamics, with recent demonstrations achieving 30% improvement in reacquisition times compared to conventional methods.

## 4.6 Conclusion

The analysis reveals three principal findings regarding LEO navigation systems. First, Doppler management remains the primary technical challenge, requiring receiver processing capabilities substantially beyond current GNSS designs. Second, economic viability depends critically on dual-use infrastructure models that combine communication and navigation services. Third, successful deployment requires international standardization efforts addressing signal interoperability and spectrum sharing between LEO and GNSS systems. Future development should prioritize open signal interfaces, dynamic spectrum management frameworks, and multi-constellation interoperability standards to realize the full potential of LEO navigation augmentation.


# Task 5
GenAI: Deepseek

link: [https://github.com/Togure/AAE-6102-Assignment-2/edit/main/deepseek-Task5.png](https://github.com/Togure/AAE-6102-Assignment-2/blob/main/deepseek-Task5.png)
## 5.1 The Role of GNSS Interferometric Reflectometry in Geometric Remote Sensing

Global Navigation Satellite System Interferometric Reflectometry (GNSS-IR) has emerged as a transformative technique in remote sensing, leveraging reflected GNSS signals to measure geometric and environmental parameters. Originally developed to augment traditional positioning, GNSS-IR now enables precise measurements of sea level, land surface heights, and even the dimensions of man-made structures. This essay explores the principles of GNSS-IR with a focus on geometric applications—particularly altimetry and height estimation—while contextualizing its broader utility in soil moisture and vegetation monitoring.

## 5.2 Principles of GNSS-IR for Geometric Measurements

The core principle of GNSS-IR lies in analyzing interference patterns between direct GNSS signals and those reflected off surfaces like water, soil, or buildings. When a GNSS receiver captures both the direct line-of-sight signal and its ground-reflected counterpart, their interaction produces oscillations in the signal-to-noise ratio (SNR) data. These oscillations encode information about the vertical distance between the antenna and the reflecting surface. By decomposing SNR data into frequency components, the reflector height can be derived from the dominant interference frequency. For instance, a sea surface or flat roof generates coherent reflections, allowing phase delays to be converted into precise height measurements. This method relies on the geometric relationship between the satellite elevation angle, antenna height, and the path difference of the reflected signal.

## 5.3 Geometric Applications: Sea Level and Structural Height

One of the most established applications of GNSS-IR is sea level altimetry [8]. Coastal GNSS stations, often installed for geodetic purposes, can double as tide gauges by analyzing reflections from the water surface. As tides rise or fall, the path length of the reflected signal changes, altering the interference frequency in the SNR data. Studies demonstrate that GNSS-IR can achieve sub-centimeter accuracy in sea level measurements when calibrated against traditional tide gauges. For example, the Plate Boundary Observatory in Alaska uses GNSS-IR to monitor tidal variations, complementing satellite altimetry in regions with sparse instrumentation.

Similarly, GNSS-IR can estimate the height of adjacent structures when antennas are mounted on buildings or towers. If a GNSS antenna is installed on a rooftop, reflections from nearby surfaces (e.g., another building or the ground) produce SNR patterns that reveal the relative height difference. This technique has been validated in urban environments, where it aids in 3D mapping without LiDAR. However, accuracy depends on surface roughness; flat, horizontal reflectors yield the most reliable results.

## 5.4 Geometric Applications: Distance to the Building's Reflection Surface
In urban-area GNSS positioning, the reflection of GNSS signal can be modeled to mitigate the positioning impair derived from multipath effect. To simulate the signal propagation process, the distance from the receiver to the building surface is critical to be calculated. This requirement can be achieved by GNSS-IR [9], which is similar to the sea-level detection. Therefore, GNSS-IR has potential to be applied in environment constructure and GNSS positioning.


## 5.5 Advantages Over Conventional Methods

GNSS-IR offers unique advantages for geometric remote sensing [10]. Unlike radar or LiDAR, it requires no dedicated transmitter, leveraging existing GNSS constellations like GPS or Galileo. This makes it a low-cost solution for continuous monitoring. Its temporal resolution—often minutes to hours—surpasses that of satellite-based altimetry, capturing dynamic processes like storm surges or structural settling. Moreover, GNSS-IR operates in all weather conditions, unaffected by clouds or darkness, a limitation of optical techniques.

## 5.6 Broader Context: Soil Moisture and Vegetation

While geometric measurements are a strength of GNSS-IR, the technique also contributes to environmental monitoring. Soil moisture affects the dielectric properties of the ground, altering the amplitude and phase of reflected GNSS signals. By tracking these changes, GNSS-IR provides estimates of volumetric water content in the topsoil layer, useful for agriculture and hydrology. Vegetation monitoring, though less precise than geometric applications, is possible through signal attenuation analysis. Dense canopies scatter reflections, reducing SNR coherence, which can correlate with biomass or crop growth stages. These applications, however, require empirical calibration and are secondary to GNSS-IR’s primary role in height/distance measurement.

## 5.7 Challenges and Limitations

Despite its promise, GNSS-IR faces geometric constraints. Surface roughness—such as ocean waves or uneven terrain—introduces noise, degrading measurement accuracy. Low-elevation satellite signals (5°–30° above the horizon) are ideal for reflections but are susceptible to multipath interference from obstacles. Spatial resolution is another limitation; the footprint of a GNSS-IR measurement spans hundreds of square meters, making it unsuitable for fine-scale mapping. Validation also remains critical, as site-specific factors (e.g., antenna gain pattern) require ground-truth data for calibration.

## 5.8 Future Directions

Advancements in multi-frequency GNSS (e.g., GPS L5, Galileo E5) promise to mitigate interference and improve precision. Integrating GNSS-IR with unmanned aerial vehicles (UAVs) could enable mobile height profiling, while urban IoT networks might adopt the technique for infrastructure monitoring. Hybrid approaches, combining GNSS-IR with synthetic aperture radar (SAR), are also being explored to compensate for individual limitations.

## 5.9 Conclusion

GNSS-IR has carved a niche in geometric remote sensing, offering a passive, cost-effective means to measure sea levels, structural heights, and land surface dynamics. While its applications in soil moisture and vegetation monitoring are noteworthy, its precision in altimetry and height estimation sets it apart from conventional methods. As GNSS constellations evolve and algorithms mature, GNSS-IR could democratize access to high-frequency geometric data, bridging gaps in global environmental and urban monitoring systems.

# Reference List
[1] Hofmann-Wellenhof B, Lichtenegger H, Wasle E. GNSS–global navigation satellite systems: GPS, GLONASS, Galileo, and more[M]. Springer Science & Business Media, 2007.

[2] Takasu T, Yasuda A. Development of the low-cost RTK-GPS receiver with an open source program package RTKLIB[C]//International symposium on GPS/GNSS. Seogwipo-si, Republic of Korea: International Convention Center Jeju Korea, 2009, 1: 1-6.

[3] Zumberge J F, Heflin M B, Jefferson D C, et al. Precise point positioning for the efficient and robust analysis of GPS data from large networks[J]. Journal of geophysical research: solid earth, 1997, 102(B3): 5005-5017.

[4] Wabbena G, Schmitz M, Bagge A. PPP-RTK: precise point positioning using state-space representation in RTK networks[C]//Proceedings of the 18th international technical meeting of the satellite division of the Institute of navigation (ION GNSS 2005). 2005: 2584-2594.

[5] R. G. Brown, G. Y. Chin, and J. H. Kraemer, “RAIM: Will It Meet the RTCA GPS Minimum Operational Performance Standards?” in Proceedings of the 1991 National Technical Meeting of The Institute of Navigation, 1991, pp. 103–111. [Online]. Available: https://www.ion.org/publications/abstract.cfm?articleID=5020

[6] Prol F S, Ferre R M, Saleem Z, et al. Position, navigation, and timing (PNT) through low earth orbit (LEO) satellites: A survey on current status, challenges, and opportunities[J]. IEEE access, 2022, 10: 83971-84002.

[7] Zhao X, Zhou S, Ci Y, et al. High-precision orbit determination for a LEO nanosatellite using BDS-3[J]. GPS Solutions, 2020, 24: 1-14.

[8] Larson K M, Löfgren J S, Haas R. Coastal sea level measurements using a single geodetic GPS receiver[J]. Advances in space research, 2013, 51(8): 1301-1310.

[9] Ye M, Zhang G, Hsu L T. Building model rectification using GNSS reflectometry[J]. IEEE Geoscience and Remote Sensing Letters, 2024.

[10] Chew C C, Small E E, Larson K M, et al. Effects of near-surface soil moisture on GPS SNR data: Development of a retrieval algorithm for soil moisture[J]. IEEE Transactions on Geoscience and Remote Sensing, 2013, 52(1): 537-543.

