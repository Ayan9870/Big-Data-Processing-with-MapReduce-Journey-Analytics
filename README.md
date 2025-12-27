# Big Data Processing with MapReduce, Journey Analytics

---

## Project Overview

MapReduce programs using Hadoop and Python to efficiently process and analyze large-scale taxi trip data. The programs perform distributed computation to extract key insights such as trip duration statistics, peak hours, popular pickup and drop-off locations, and fare trends. Leveraging the parallel processing capabilities of the Hadoop ecosystem, the solution is optimised for scalability and performance in handling high-volume transportation datasets.

---

## Access to Code 🔒

The source code for this project is **private** and available upon request.

If you're an **employer** or **recruiter** and would like to review the code, please **request access via email** at **ayanhashmi205@yahoo.com**.

---

## Installation 📦

#### Prerequisites
- AWS EMR cluster with Hadoop 3.1.4
- Python 3.x
- HDFS access

#### Setup Data Files

```bash
# Upload data files to HDFS
hdfs dfs -mkdir /Input
hdfs dfs -put Trips.txt /Input/
hdfs dfs -put Taxis.txt /Input/
```

#### Clone and Run

```bash
# Clone the repository
git clone https://github.com/ayan9870/big-data-taxi-analytics.git
cd big-data-taxi-analytics

# Run individual Modules
bash Module1-run.sh
bash Module2-run.sh  
bash Module3-run.sh
```

---

## Features 📋

* **Module 1**: Trip statistics analysis with in-mapper combining
  - Categorizes trips by distance (short <100, medium 100-200, long ≥200)
  - Calculates count, max fare, min fare, and average fare per taxi
  - Implements state preservation across mapper lines

* **Module 2**: K-medoid clustering using PAM algorithm
  - Clusters trips based on dropoff locations
  - Configurable k-value and iteration count via initialization.txt
  - Euclidean distance-based dissimilarity measure

* **Module 3**: Multi-stage MapReduce pipeline
  - Join operation between Trips.txt and Taxis.txt
  - Company-wise trip counting
  - Ascending sort by total trip count

* **Scalability**: All Modules designed for 3 reducers and big data processing
* **Documentation**: Comprehensive comments and clear program flow

---

## Architecture 🏗️

### MapReduce Pipeline Design

#### Module 1: Trip Statistics Analysis
```
Mapper → In-memory Combining → Partitioner → Reducer
```
- **Input**: Trips.txt
- **Output**: Statistics per taxi and trip type
- **Key Feature**: State preservation across mapper lines

#### Module 2: K-medoid Clustering  
```
Initialization → Assignment → Update → Iteration → Convergence
```
- **Input**: Trips.txt + initialization.txt
- **Output**: Clustered trip dropoff locations
- **Algorithm**: Partitioning Around Medoids (PAM)

#### Module 3: Company Trip Analysis
```
Join Stage → Count Stage → Sort Stage
```
- **Input**: Trips.txt + Taxis.txt
- **Output**: Companies sorted by trip count
- **Pipeline**: Three sequential MapReduce jobs

---

## Technical Specifications ⚙️

### Requirements
- **Language**: Python 3.x only (no Java, no mrjob library)
- **Platform**: AWS EMR with Hadoop 3.1.4
- **Reducers**: Configured for 3 reducers across all Modules
- **Memory**: Line-by-line processing (no complete dataset in memory)

### HDFS Directory Structure
```
/Input/
├── Trips.txt
└── Taxis.txt

/Output/
├── Module1/
├── Module2/
└── Module3/
```

### Performance Considerations
- In-mapper combining for reduced I/O overhead
- Partitioning strategy optimized for 3 reducers
- Memory-efficient streaming processing
- Configurable clustering parameters

---

## Algorithm Details 🔍

### K-medoid Clustering (PAM)
1. **Initialize**: Randomly select k medoids from dropoff locations
2. **Assignment**: Associate each trip to closest medoid (Euclidean distance)
3. **Update**: Find optimal medoid with lowest total cost configuration
4. **Iteration**: Repeat until convergence or maximum iterations reached

### Trip Categorization Logic
- **Short trips**: distance < 100 units
- **Medium trips**: 100 ≤ distance < 200 units  
- **Long trips**: distance ≥ 200 units

---

## Results Summary 📈

| Module | Processing Type | Output | Complexity |
|------|----------------|---------|------------|
| Module 1 | Single MapReduce | Trip statistics per taxi | O(n) |
| Module 2 | Iterative MapReduce | Clustered locations | O(k*v*n²) |
| Module 3 | Multi-stage Pipeline | Sorted company counts | O(n log n) |

---

## Author ✨

| <a href="https://github.com/ayan9870" target="_blank">**Muhammad Ayan Hashmi**</a> |
|:--:|
| ![Ayan Hashmi](https://github.com/ayan9870.png?size=100) |
| [`github.com/ayan9870`](https://github.com/ayan9870) |

---

## License
[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

- **[MIT license](http://opensource.org/licenses/mit-license.php)**
