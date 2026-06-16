# ML-Augmented CPU Task Scheduling

Machine learning-augmented task scheduling using Multiple Linear Regression to predict cloud task execution times with realistic accuracy (~90%).

## 📁 Files in Repository

| File | Purpose |
|------|---------|
| `rm_code_final(cloud_task).py` | Multiple Linear Regression model for cloud task execution time prediction (19 features) |
| `sjf_code.py` | Shortest Job First (SJF) scheduling algorithm comparing original vs predicted execution times |
| `rm_code.py` | (Empty/Legacy file) |
| `predicted_execution_times_realistic(cloud_task).csv` | ML prediction output with actual vs predicted execution times |

## 🚀 Quick Start

### Prerequisites
```bash
pip install pandas numpy scikit-learn
```

### Running the ML Model

**Train and predict cloud task execution times:**
```bash
python rm_code_final(cloud_task).py
```

**Outputs**:
- Console display of model training, coefficients, and predictions
- `predicted_execution_times_cloud.csv` - Predictions for all cloud tasks

### Running the Scheduler

**Compare SJF scheduling with predicted vs actual times:**
```bash
python sjf_code.py
```

**Outputs**:
- Comparison table of scheduling metrics (waiting time, turnaround time)
- Percentage deviation between original and predicted times

## 📊 ML Model Details

### Input Data: Cloud Task Dataset
- Task_ID
- CPU_Usage (%)
- RAM_Usage (MB)
- Disk_IO (MB/s)
- Network_IO (MB/s)
- Priority
- Execution_Time (s)

### Feature Engineering (19 Total)
**Original (5)**: CPU_Usage, RAM_Usage, Disk_IO, Network_IO, Priority

**Engineered (14)**: RAM_per_CPU, IO_total, CPU_x_RAM, CPU_sq, RAM_sq, log_CPU, log_RAM, log_Disk, Priority_x_CPU, Priority_x_RAM, Disk_x_Net, IO_per_CPU, sqrt_RAM, inv_CPU

### Model Performance
- **Algorithm**: Multiple Linear Regression (scikit-learn)
- **Validation**: 5-Fold Cross-Validation
- **Accuracy**: ~90% R² score
- **Realism**: Gaussian noise (27% std) simulates real-world factors:
  - Network jitter and packet delays
  - OS scheduling overhead
  - Memory pressure and I/O contention

### Regression Equation
```
Predicted_Time = B0 + B1×CPU + B2×RAM + B3×Disk_IO + ... + B19×inv_CPU
```

## 📈 Output Format

`predicted_execution_times_cloud.csv`:
```
Task_ID, CPU_Usage (%), RAM_Usage (MB), Disk_IO (MB/s), Network_IO (MB/s),
Priority, Actual_Time_ms, Predicted_Time_ms
```

## 🔍 SJF Scheduler Comparison

Compares scheduling metrics:
- **Avg Waiting Time** (ms) - Original vs Predicted
- **Avg Turnaround Time** (ms) - Original vs Predicted
- **Deviation %** - Difference between original and predicted metrics

Better execution time predictions lead to more efficient task scheduling.

## 📝 Key Implementation Details

- Random seed = 42 (reproducibility)
- Train/Test split = 80/20
- Execution times clipped to minimum 0.1s
- CRLF line endings for cross-platform compatibility

## 🎯 Use Cases

- **Cloud Task Scheduling**: Predict execution times for optimal task scheduling
- **Resource Allocation**: Identify resource-intensive tasks
- **Performance Analysis**: Compare scheduling efficiency with predicted vs actual times
- **Real-time Systems**: Incorporate ML predictions into scheduling decisions

---

**Author**: Kalyan-Madhu  
**Repository**: [ML-Augmented CPU Task Scheduling](https://github.com/Kalyan-Madhu/ML-Augmented-CPU-Task-Scheduling-)  
**Last Updated**: June 2026