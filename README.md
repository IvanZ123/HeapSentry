# HeapSentry

This project, the HeapSentry, aims to detect and prevent malicious heap overflows by adding canaries at the end of each heap object and checking by the kernel before system calls executed. The attacker model of HeapSentry includes both Control-data attacks and Non-control-data-attacks. The implementation of HeapSentry can be divided into two components: *HeapSentry-U* and *HeapSentry-K*.
HeapSentry-U works in user space and intercepts memory allocation functions. It adds cannaries in each allocated block, then passes the address and value of the canary to HeapSentry-K. HeapSentry-K works in kernel space and stores the information of canaries. It will only be loaded when a system call is generated, including implemented system calls such as *fork* and unimplemented system calls which is used for the communication between HeapSentry-U and HeapSentry-K. HeapSentry-K compares current canary with oringinal one and decides whether to terminate the calling process or not.