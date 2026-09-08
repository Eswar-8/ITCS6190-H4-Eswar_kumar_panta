# Hands-on L4 — Report

**Name:** Eswar kumar panta

**Student ID:** 801505751

**Email:** epanta@charlotte.edu

---

## What I ran

The commands you used, in the order you used them. If you deviated from the steps in the
README, say where and why.

```bash
# 1. Start the Hadoop cluster
docker compose up -d

# 2. Build the project
mvn clean package

# 3. Copy the JAR into the ResourceManager container
docker cp target/WordCountUsingHadoop-0.0.1-SNAPSHOT.jar resourcemanager:/tmp/

# 4. Copy your dataset into the container
docker cp shared-folder/input/data/input.txt resourcemanager:/tmp/

# 5-9. Open shell, load data, run job, view results, and copy to container exit path
docker exec -it resourcemanager bash '
  cd /tmp
  hadoop fs -mkdir -p /input/data
  hadoop fs -put ./input.txt /input/data
  hadoop fs -ls /input/data
  hadoop jar /tmp/WordCountUsingHadoop-0.0.1-SNAPSHOT.jar \
    com.example.controller.Controller /input/data/input.txt /output
  hadoop fs -cat /output/*
  hdfs dfs -get /output /tmp/
  exit

# 10. Copy the results back to your local machine
docker cp resourcemanager:/tmp/output/. shared-folder/output/

# 11. Stop the cluster
docker compose down
```

---

## Input and output

### My input dataset

```Distributed Systems Overview
Distributed computing frameworks allow massive datasets to be processed across clusters of commodity hardware. By breaking down large workloads into smaller, independent tasks, systems can execute operations in parallel. The map phase filters and transforms individual data records into intermediate key-value pairs, while the reduce phase aggregates and summarizes these intermediate results. Fault tolerance and data locality remain core design principles for ensuring high availability and performance in large-scale distributed architectures.

Data Pipeline Analytics
Real-time data streaming and batch processing form the backbone of modern analytics pipelines. Sensor feeds, log files, and transactional records continuously generate petabytes of unstructured information. Efficient ingestion mechanisms require robust partitioning strategies to prevent network bottlenecks and memory overflow. Engineers continuously monitor latency, throughput, and error rates to maintain optimal resource utilization across distributed nodes.

General Narrative Text
The morning mist rolled softly over the rolling green hills, obscuring the old stone bridge that crossed the rushing river. Travelers from distant towns often paused here to rest their horses and share stories of the open road. As the sun climbed higher into the clear blue sky, the shadows receded, revealing the vibrant wildflowers blooming along the winding path. Every season brought its own unique charm, drawing both wanderers and dreamers seeking peace away from the bustling city streets.

```

### The output the job produced

Paste the contents of your output file here.

```
the	12
and	10
data	3
into	3
from	2
phase	2
distributed	2
intermediate	2
Distributed	2
records	2
continuously	2
The	2
across	2
hills,	1
peace	1
its	1
workloads	1
optimal	1
datasets	1
strategies	1
large	1
clusters	1
rest	1
over	1
softly	1
drawing	1
rates	1
Fault	1
core	1
high	1
summarizes	1
down	1
Efficient	1
seeking	1
Every	1
dreamers	1
independent	1
for	1
filters	1
hardware.	1
unstructured	1
Overview	1
can	1
petabytes	1
Pipeline	1
green	1
files,	1
nodes.	1
utilization	1
pairs,	1
stone	1
both	1
mist	1
brought	1
path.	1
share	1
higher	1
pipelines.	1
robust	1
availability	1
here	1
Sensor	1
systems	1
blooming	1
modern	1
bridge	1
away	1
Travelers	1
Analytics	1
generate	1
streets.	1
prevent	1
maintain	1
Narrative	1
breaking	1
vibrant	1
Data	1
overflow.	1
processed	1
Systems	1
bustling	1
these	1
Engineers	1
that	1
execute	1
morning	1
mechanisms	1
require	1
individual	1
shadows	1
wanderers	1
crossed	1
rushing	1
form	1
computing	1
road.	1
wildflowers	1
often	1
old	1
open	1
operations	1
reduce	1
towns	1
principles	1
river.	1
revealing	1
throughput,	1
ensuring	1
bottlenecks	1
backbone	1
parallel.	1
architectures.	1
remain	1
batch	1
rolled	1
key-value	1
log	1
large-scale	1
while	1
stories	1
smaller,	1
monitor	1
sun	1
design	1
their	1
clear	1
map	1
results.	1
massive	1
transforms	1
transactional	1
along	1
climbed	1
season	1
analytics	1
aggregates	1
charm,	1
feeds,	1
network	1
city	1
receded,	1
rolling	1
allow	1
Real-time	1
horses	1
processing	1
latency,	1
error	1
unique	1
ingestion	1
frameworks	1
blue	1
distant	1
own	1
winding	1
memory	1
obscuring	1
sky,	1
tolerance	1
locality	1
General	1
information.	1
streaming	1
commodity	1
tasks,	1
Text	1
performance	1
partitioning	1
paused	1
resource	1
```

---

## What I observed

A few sentences on what happened while the job was running. Pick whatever you actually
noticed. Some things worth looking at:

- How long the map phase took compared with the reduce phase
- How many DataNodes showed as live at <http://localhost:9870>
- What the ResourceManager at <http://localhost:8088> showed during the run
- Whether the output ordering matched what you expected



---

## Problems and fixes

Anything that went wrong and what resolved it. Paste the actual error message. If nothing
went wrong, say so.


