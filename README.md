# Reliable-Transport-Protoccol

For this project, we designed a simple transport protocol that provides reliable datagram service using UDP. The protocol is responsible for ensuring data is delivered in order and efficiently through duplicated, dropped, delayed, or corrupted packets, and changing bandwidths and latencies. Our code is tested using a simulator which functions as a virtual machine that emulates an unreliable network with varying levels of difficulty and expected implemented behavior. The `test` and `run` scripts evaluates our code against the test cases in the `configs` folder.


