---
title: "Peak Memory Usage"
date: 2022-03-15
categories: linux
---

## __1. Checking Peak Memory Usage

 - How to : /usr/bin/time -v command
    - Maximum resident set size(Maximum RSS) : Peak Memory Usage
     - https://stackoverflow.com/questions/774556/peak-memory-usage-of-a-linux-unix-process/774601#774601

 - Resident set size(RSS)
    - "resident set size (RSS) is the portion of memory occupied by a process that is held in main memory (RAM)"
    - https://en.wikipedia.org/wiki/Resident_set_size
    - https://stackoverflow.com/a/60779604

 - test commands
```
[hrs@node36 test_case]$ /usr/bin/time  -v awk 'BEGIN{for(i=1;i<=111120;i++)a[i]=i}'
        Command being timed: "awk BEGIN{for(i=1;i<=111120;i++)a[i]=i}"
        User time (seconds): 0.03
        System time (seconds): 0.01
        Percent of CPU this job got: 97%
        Elapsed (wall clock) time (h:mm:ss or m:ss): 0:00.04
        Average shared text size (kbytes): 0
        Average unshared data size (kbytes): 0
        Average stack size (kbytes): 0
        Average total size (kbytes): 0
        Maximum resident set size (kbytes): 22424
        Average resident set size (kbytes): 0
        Major (requiring I/O) page faults: 0
        Minor (reclaiming a frame) page faults: 5727
        Voluntary context switches: 1
        Involuntary context switches: 1
        Swaps: 0
        File system inputs: 0
        File system outputs: 0
        Socket messages sent: 0
        Socket messages received: 0
        Signals delivered: 0
        Page size (bytes): 4096
        Exit status: 0
```
```
[hrs@node36 test_case]$ /usr/bin/time  -v awk 'BEGIN{for(i=1;i<=1111120;i++)a[i]=i}'
        Command being timed: "awk BEGIN{for(i=1;i<=1111120;i++)a[i]=i}"
        User time (seconds): 0.43
        System time (seconds): 0.09
        Percent of CPU this job got: 99%
        Elapsed (wall clock) time (h:mm:ss or m:ss): 0:00.52
        Average shared text size (kbytes): 0
        Average unshared data size (kbytes): 0
        Average stack size (kbytes): 0
        Average total size (kbytes): 0
        Maximum resident set size (kbytes): 213824
        Average resident set size (kbytes): 0
        Major (requiring I/O) page faults: 0
        Minor (reclaiming a frame) page faults: 53964
        Voluntary context switches: 1
        Involuntary context switches: 1
        Swaps: 0
        File system inputs: 0
        File system outputs: 0
        Socket messages sent: 0
        Socket messages received: 0
        Signals delivered: 0
        Page size (bytes): 4096
        Exit status: 0

```

