# Braking Variability Analysis Under Different Driving Conditions

## Using Argoverse 2 Motion Forecasting Dataset

### A Data Science Project using Conditional Time Series Analysis and Scenario-wise Comparison

---

## Project Overview

This project analyzes braking behavior variability across different driving conditions using real-world autonomous vehicle trajectory data. The study employs conditional time series analysis, statistical hypothesis testing, and change point detection to understand how contextual factors influence vehicle deceleration patterns.

---

## My Details

| Name | Roll Number | Email |
|------|-------------|-------|
| Shraddha Sahni | 1024230044 | [ssahni_be24@thapar.edu] |

---

## Institution

**Thapar Institute of Engineering and Technology**  
*(Deemed to be University)*  
Department of Computer Science and Engineering  
Patiala, Punjab, India

---

## Dataset

**Name:** Argoverse 2 Motion Forecasting Dataset  
**Source:** Argo AI  
**Link:** https://www.argoverse.org/av2.html  
**Type:** Real-world autonomous vehicle trajectory data  
**Format:** Parquet files with scenario-based organization

### Dataset Structure

data/
├── train/
│ ├── 0000b0f9-99f9-4a1f-a231-5be9e4c523f7/
│ │ ├── scenario_0000b0f9-....parquet
│ │ └── log_map_archive_....json
│ └── ...
├── val/
│ └── ...
└── test/
└── ..


---

## Project Objectives

1. Extract and preprocess vehicle trajectory data from the Argoverse dataset
2. Compute motion dynamics (velocity, acceleration, jerk) from positional time-series
3. Identify and quantify braking events using deceleration-based indicators
4. Perform conditional time series analysis of braking behavior
5. Conduct scenario-wise comparison (straight vs. turning vs. stopping)
6. Analyze braking transition points using change-point detection
7. Derive statistical insights on braking variability and risk patterns
8. Visualize and interpret behavioral differences across scenarios

---

## 🔧 Methodology

### 1. Feature Engineering
- Velocity computation from trajectory coordinates
- Acceleration derivation using temporal differentiation
- Jerk calculation (rate of change of acceleration)
- Heading angle and heading change computation
- Speed category segmentation (stopped, slow, moderate, fast, very_fast)

### 2. Braking Event Detection
| Severity | Threshold | Description |
|----------|-----------|-------------|
| Mild | < -1.0 m/s² | Gentle braking |
| Moderate | < -2.5 m/s² | Normal braking |
| Hard | < -4.5 m/s² | Emergency braking |

### 3. Conditional Time Series Analysis
- Rolling mean and standard deviation
- Time-dependent braking variability
- Condition-based segmentation by speed and scenario type

### 4. Scenario Classification
- **Straight:** Heading change < 0.5 radians
- **Turning:** Heading change ≥ 0.5 radians
- **Stopping:** Maximum velocity < 1.0 m/s

### 5. Change Point Detection
- Algorithm: PELT (Pruned Exact Linear Time)
- Library: `ruptures` with RBF kernel
- Purpose: Detect behavioral transitions (cruise → brake → resume)

### 6. Statistical Analysis
- Descriptive statistics (mean, std, min, max, IQR, CV)
- Welch's t-test for mean comparison
- Mann-Whitney U test for non-parametric comparison
- Cohen's D for effect size measurement
- Levene's test for variance equality

---

## Project Structure

braking_variability_project/
│
├── data/
│ ├── train/ # Training split parquet files
│ ├── val/ # Validation split parquet files
│ └── test/ # Test split parquet files
│
├── notebooks/
│ └── braking_analysis.ipynb # Main analysis notebook (40+ cells)
│
├── outputs/
│ ├── plots/ # All generated visualizations (16+ plots)
│ │ ├── 01_raw_trajectories.png
│ │ ├── 02_kinematics_.png
│ │ ├── 03_braking_detection.png
│ │ ├── 04_severity_distribution.png
│ │ ├── 05_rolling_statistics.png
│ │ ├── 06_conditional_speed.png
│ │ ├── 07_scenario_comparison_boxplots.png
│ │ ├── 08_severity_heatmap.png
│ │ ├── 09_distribution_analysis.png
│ │ ├── 10_change_points.png
│ │ ├── 11_change_point_statistics.png
│ │ ├── 12_deep_dive_.png
│ │ ├── 13_correlation_heatmap.png
│ │ ├── 14_velocity_vs_deceleration.png
│ │ ├── 15_city_comparison.png
│ │ ├── 16_summary_dashboard.png
│ │ ├── A_braking_patterns.png
│ │ ├── B_braking_variability_quantitative.png
│ │ ├── C_transition_points.png
│ │ ├── D_contextual_factors.png
│ │ └── MASTER_braking_variability_analysis.png
│ │
│ └── reports/ # Generated text reports
│ └── braking_analysis_report.txt
│
├── README.md # This file
└── requirements.txt # Python dependencies


---

## ⚙️ Installation

### Prerequisites
- Python 3.8 or higher
- pip package manager
- Jupyter Notebook or JupyterLab

### Step 1: Clone/Download Project
cd braking_variability_project

### Step 2: Create Virtual Environment

python -m venv venv
# On Windows
venv\Scripts\activate

# On macOS/Linux
source venv/bin/activate

### Step 3: Install Dependencies
pip install -r requirements.txt

### Step 4: Download Dataset
Visit: https://www.argoverse.org/av2.html
Register and download the Motion Forecasting dataset
Extract to data/train/, data/val/, data/test/ folders

### Step 5: Run the Notebook
jupyter notebook notebooks/braking_analysis.ipynb

### Requirements
numpy>=1.24.0
pandas>=2.0.0
matplotlib>=3.7.0
seaborn>=0.12.0
scipy>=1.11.0
scikit-learn>=1.3.0
ruptures>=1.1.7
tqdm>=4.65.0
pyarrow>=12.0.0
jupyter>=1.0.0
Install with:

pip install -r requirements.txt

### Key Results
Braking Variability by Scenario Type
Metric	Straight	Turning	
Mean Peak Decel (m/s²)	-1.2 to -2.5	-2.0 to -4.0	
Coefficient of Variation	~15-25%	~25-40%	
Braking Ratio	0.10-0.20	0.20-0.35	
Hard Braking %	Lower	Higher	

### Statistical Significance
Peak Deceleration: p < 0.05 (Significant)
Braking Ratio: p < 0.05 (Significant)
Effect Size (Cohen's D): Medium to Large

### Change Point Detection
Average transitions per scenario: 2-5
Successfully identifies braking onset/offset
Validates behavioral shift detection

### Generated Outputs
Visualizations (16+ Plots)
Raw trajectory visualization
Kinematic feature profiles (velocity, acceleration, jerk)
Braking event detection with thresholds
Severity distribution (pie + bar charts)
Rolling statistics time series
Conditional braking by speed category
Scenario-wise comparison boxplots
Severity heatmap
Distribution analysis (histograms + violin)
Change point detection visualization
Change point statistics by type
Deep dive 4-panel analysis
Feature correlation heatmap
Velocity vs deceleration scatter
City-wise comparison
Summary dashboard
Master variability analysis (12-panel)

### Reports
Comprehensive text report with all findings
Statistical test results
Conclusions and insights

### Key Findings
Braking behavior differs significantly between straight and turning scenarios
Turning scenarios involve more frequent and intense braking events
Higher vehicle speeds correlate with stronger peak deceleration
Change point detection successfully identifies behavioral transitions
Rolling statistics reveal time-dependent braking variability patterns
Hard braking events are more common during complex maneuvers
Conditional analysis shows braking severity increases with speed
City-specific variations in braking patterns were observed

@misc{sahni2024braking,
  title={Analyze Braking Variability Under Different Driving Conditions Using Argoverse Motion Forecasting Dataset},
  author={Sahni, Shraddha and Kaur, Rehmat},
  year={2024},
  publisher={Thapar Institute of Engineering and Technology},
  note={Department of Computer Science and Engineering}
}

### Limitations
Analysis limited to focal agent trajectories only
Braking thresholds based on literature, not ground-truth calibrated
Weather and road condition metadata not incorporated
City-specific analysis limited by dataset availability
Multi-agent interaction effects not fully explored

### Future Work
Incorporate multi-agent interaction analysis
Add weather and road condition contextual factors
Develop ML model to predict braking severity
Extend to real-time braking behavior monitoring
Calibrate thresholds using ground-truth brake pedal data
Analyze pedestrian and cyclist braking patterns
Include map topology and traffic signal information

### Contact
For questions or collaboration:
Shraddha Sahni: [ssahni_be24@thapar.edu]

### License
This project is for academic and research purposes.
Argoverse 2 dataset is subject to its own license terms: https://www.argoverse.org/av2.html

### Acknowledgments
Argo AI for providing the Argoverse 2 Motion Forecasting Dataset
Thapar Institute of Engineering and Technology for academic support
Department of Computer Science and Engineering for guidance

### GitHub badge
[![GitHub stars](https://img.shields.io/github/stars/Shraddha-Sahni/braking-variability)](https://github.com/Shraddha-Sahni braking-variability-project.git)
