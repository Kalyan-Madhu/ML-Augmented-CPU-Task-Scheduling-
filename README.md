# ML-Augmented CPU Task Scheduling

A machine learning-based approach to predicting task execution times and optimizing CPU task scheduling using Multiple Linear Regression. This project implements both traditional scheduling algorithms (Rate Monotonic and Shortest Job First) augmented with ML-predicted execution times for improved accuracy in real-world environments.

## 📋 Project Overview

This project addresses the challenge of predicting task execution times in CPU-bound and cloud task environments by:

1. **Building ML models** that predict task execution times based on resource requirements
2. **Incorporating real-world variability** (network jitter, OS overhead, memory contention, I/O delays)
3. **Evaluating scheduling algorithms** (RM and SJF) with both original and predicted execution times
4. **Achieving ~90% accuracy** through feature engineering and realistic noise simulation

### Key Features

- **Multiple Linear Regression** for execution time prediction
- **19 engineered features** (5 original + 14 derived features)
- **5-Fold Cross-Validation** for robust model evaluation
- **Realistic noise modeling** (27% standard deviation) simulating real-world factors
- **Two datasets**: Cloud tasks and OS CPU-bound processes
- **Scheduling comparison** between actual and predicted execution times

## 📁 Project Structure

```
├── rm_code.py                                          # (Empty/Legacy)
├── rm_code_final(OS_cbp).py                          # Rate Monotonic scheduling for OS processes
├── rm_code_final(cloud_task).py                      # Rate Monotonic scheduling for cloud tasks
├── sjf_code.py                                        # Shortest Job First scheduling algorithm
├── cloud_task_scheduling_dataset.csv                 # Cloud task dataset (original)
├── OS_cbp_corrected.csv                              # OS CPU-bound processes dataset
├── predicted_execution_times_realistic(cloud_task).csv  # ML predictions for cloud tasks
├── predicted_execution_times_realistic(OS_cbp).csv     # ML predictions for OS processes
└── README.md                                          # This file
```

## 🎯 Datasets

### Cloud Task Scheduling Dataset
- **File**: `cloud_task_scheduling_dataset.csv`
- **Features**:
  - Task_ID
  - CPU_Usage (%)
  - RAM_Usage (MB)
  - Disk_IO (MB/s)
  - Network_IO (MB/s)
  - Priority
  - Execution_Time (s)

### OS CPU-Bound Processes Dataset
- **File**: `OS_cbp_corrected.csv`
- **Features**:
  - Job_ID
  - Job_Size_MI
  - CPU_Required
  - RAM_Required_GB
  - Priority_Class
  - Estimated_Time_Sec

## 🤖 Machine Learning Models

### Feature Engineering (19 Total Features)

**Original Features (5)**:
- CPU_Usage
- RAM_Usage
- Disk_IO
- Network_IO
- Priority

**Engineered Features (14)**:
- RAM_per_CPU = RAM_Usage / CPU_Usage
- IO_total = Disk_IO + Network_IO
- CPU_x_RAM = CPU_Usage × RAM_Usage
- CPU_sq = CPU_Usage²
- RAM_sq = RAM_Usage²
- log_CPU = log(CPU_Usage)
- log_RAM = log(RAM_Usage)
- log_Disk = log(Disk_IO + 1)
- Priority_x_CPU = Priority × CPU_Usage
- Priority_x_RAM = Priority × RAM_Usage
- Disk_x_Net = Disk_IO × Network_IO
- IO_per_CPU = (Disk_IO + Network_IO) / CPU_Usage
- sqrt_RAM = √(RAM_Usage)
- inv_CPU = 1 / CPU_Usage

### Model Characteristics

- **Algorithm**: Multiple Linear Regression (scikit-learn)
- **Training**: 80% train / 20% test split
- **Validation**: 5-Fold Cross-Validation
- **Accuracy**: ~90% R² score
- **Realism**: Gaussian noise (σ = 27% of std) added to simulate real-world factors

## 🔧 Real-World Variability Simulation

The model incorporates realistic noise to prevent overfitting:

```
Noise represents:
- Network jitter and packet delays
- OS scheduling overhead and context switching
- Memory pressure from co-running processes
- Disk I/O contention and hypervisor interference
```

## 📊 Scheduling Algorithms

### 1. Rate Monotonic (RM)
- **File**: `rm_code_final(OS_cbp).py`, `rm_code_final(cloud_task).py`
- **Description**: Prioritizes tasks with shorter periods (higher frequency)
- **Use Case**: Real-time systems with periodic tasks

### 2. Shortest Job First (SJF)
- **File**: `sjf_code.py`
- **Description**: Executes tasks with shortest execution time first (non-preemptive)
- **Metrics**: Average Waiting Time, Average Turnaround Time
- **Comparison**: Original vs. Predicted execution times

## 📈 Output Files

- `predicted_execution_times_realistic(cloud_task).csv` - ML predictions for cloud tasks
- `predicted_execution_times_realistic(OS_cbp).csv` - ML predictions for OS processes

**Output Columns**:
- Task/Job IDs
- Resource requirements
- Actual execution time
- Predicted execution time
- Performance metrics

## 🚀 Usage

### Prerequisites
```bash
pip install pandas numpy scikit-learn
```

### Running the Models

**Cloud Task Scheduler (RM)**:
```bash
python rm_code_final(cloud_task).py
```

**OS Process Scheduler (RM)**:
```bash
python rm_code_final(OS_cbp).py
```

**SJF Scheduler**:
```bash
python sjf_code.py
```

### Output
Each script generates:
1. Dataset information
2. Feature engineering details
3. Model coefficients and regression equation
4. Cross-validation scores
5. Predicted vs. actual execution times
6. CSV file with predictions

## 📊 Model Performance

The models achieve **~90% accuracy** through:
- **Feature Engineering**: 14 engineered features capturing non-linear relationships
- **Cross-Validation**: 5-fold CV for robust evaluation
- **Realistic Noise**: 27% std deviation simulates real-world conditions
- **Comprehensive Features**: Captures CPU, memory, I/O, and priority interactions

## 🔍 Scheduling Comparison

The SJF scheduler compares performance metrics:
- **Avg Waiting Time**: Reduced with better execution time predictions
- **Avg Turnaround Time**: Improved scheduling efficiency
- **Deviation Analysis**: Percentage difference between original and predicted metrics

## 📝 Notes

- Models use `random_state=42` for reproducibility
- CRLF line endings handled for cross-platform compatibility
- Execution times clipped to minimum thresholds (0.1s for cloud, 1.0s for OS processes)
- Priority values incorporated in all scheduling decisions

## 🎓 Key Insights

1. **Prediction Accuracy**: ML models achieve realistic ~90% accuracy by incorporating real-world variability
2. **Feature Importance**: Non-linear features (quadratic, logarithmic, interactions) significantly improve predictions
3. **Scheduling Impact**: Better execution time predictions lead to more efficient task scheduling
4. **Environmental Factors**: OS overhead, network jitter, and resource contention are critical for realistic modeling

## 📚 References

- Multiple Linear Regression (scikit-learn documentation)
- Task Scheduling algorithms (Rate Monotonic, Shortest Job First)
- Real-time systems and operating system concepts

---

**Author**: Kalyan-Madhu  
**Last Updated**: June 2026