# NSS playground
nss_playground - small tool used to figure out how libc nss API works and benchmark user/group resolving via nss.

## Usage

    ./nss_playground <test> <threads> <requests> <sem-release-factor>

Parameters description:
* **test** - which function to benchmark
* **threads** - number of threads
* **requests** - number of requests to issue
* **sem-release-factor** - floating point number in [0, 1) used to determine when to release 
  semaphore for benchmark threads (how many requests should be queued before the dam will burst)
