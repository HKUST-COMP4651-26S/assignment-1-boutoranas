[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/aQEb8Lmc)
# COMP4651 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Saturday

---

### Name: BOUTOR Anas
### Student Id: 21010333
### Email: aboutor@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > The measurement tool used in my case is Phoronix Test Suite, configured in batch mode with 3 runs per test. Test suites are also limited to pts/compress-7zip for CPU compression and pts/ramspeed for memory and result uploads are disabled.
Batch mode was chosen to eliminate interactive prompts and make sure the process is fully automated and repeatable for cloud measurements. We chose only pts/compress-7zip and pts/ramspeed since it is the only focus of this assignment. And also, uploads are off to avoid extra network activity from the server instance.
For the test suite pts/compress-7zip, the results represent MIPS rating, or million instructions per second, more specifically, the average MIPS score of compression rating and decompression rating. The higher the value here, the better. And when it comes to pts/ramspeed, the resulting value is the bandwidth in MB/s. Here again, the higher the value, the better. For pts/ramspeed, I chose option number 5 for configuration (average), for a quick and focused test on bandwidth.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |  3206 MIPS               |   10209.05 MB/s                 |
    | `t2.medium`  |    7901 MIPS             |   19342.66 MB/s                 |
    | `c5d.large` |   6580 MIPS              |   14263.86 MB/s                 |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |  4850 Mbps              | 0.216 ms         |
    | `m5.large` - `m5.large`   |  9940 Mbps              | 0.227 ms         |
    | `c5n.large` - `c5n.large` |  9940 Mpbs              | 0.530 ms         |
    | `t3.medium` - `c5n.large` | 4830 Mbps               | 0.162 ms         |
    | `m5.large` - `c5n.large`  |  9940 Mbps              |  0.646 ms        |
    | `m5.large` - `t3.medium`  |  4890 Mbps             |  0.680 ms        |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |   1110 Mbps             |  55.438 ms        |
    | N. Virginia - N. Virginia |   9900 Mbps             |  0.096 ms        |
    | Oregon - Oregon           |   9940 Mbps             |  0.156 ms        |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
