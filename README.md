# Reliable-Transport-Protoccol

## About
For this project, we designed a simple transport protocol that provides reliable datagram service using UDP. The protocol is responsible for ensuring data is delivered in order and efficiently through duplicated, dropped, delayed, or corrupted packets, and changing bandwidths and latencies. Our code is tested using a simulator which functions as a virtual machine that emulates an unreliable network with varying levels of difficulty and expected implemented behavior. The `test` and `run` scripts evaluates our code against the test cases in the `configs` folder.

## Features
- ability to adapt and adjust to changing bandwidths and latencies on the sender end, changing round trip time estimation and window size
- implemented sender and receiver windows to track packets that haven't been received/haven't been acknowledge
- implemented receiver-side window functionality to re-order and send out acknowledgemnts if packets are received out of order
- added ability for sender to resend any packets that haven't been acknowledged after a timeout
- implemented functionality to detect corrupted data messages on the receiver end by hashing data message contents and try, catching the decoding of messages
- implemented functionality to detect duplicate acknowledgement messages on the senders end and ignore them
- implemented functionality to track the delay, window contents, and more throughout test cases for easier debugging

## Testing

To test the protoccol, follow these steps:

1. **Setup:** Ensure that the simulator and the associated `tests/` directory are copied into your local project directory. The simulator relies on configuration files located in this directory to define different test scenarios.

2. **Execution:** To run a test, use the following command from your terminal:

    ```bash
    ./run configs/<config-file>
    ```

    Replace `<config-file>` with the name of the configuration file corresponding to the test scenario you wish to run. Configuration files are stored in the `configs/` directory and are designed to cover a wide range of potential edge cases from dropped packets to changing bandwidths and latencies.

3. **Comprehensive Evaluation**: To evaluate the protoccol on all test cases and see it's performance, execute the following command:
    
     ```bash
    ./test
    ```
    This calls the test script in your repository which will run through all the configs and test your protoccol against them.

## Challenges

### Debugging
One of the big challenges we faced was not realizing that the simulator was checking the print statements of the sender and receiver when analyzing the expected behavior of the sender and receiver. So the simulator was incorrectly logging the receivers messages despite the messages being correctly received in our code because the print statement was located in the wrong location! 

We also faced challenges when implementing packet loss detection where the round trip estimation would repeatedly resend data messages because we forgot to account for updating the timestamp. Another challenge was efficiently implementing hashing where we attempted to use the builtin `hash` function in python, but it turns out the function generates unique hashcodes for the same string for security. Finally, we faced challenges when implementing how to grow and shrink the sender window size where we weren't sure how to grow/shrink the window based on the behavior. This was resolved once we realized that our code could handle larger window sizes.

### Performance
We haven't found a good way to effectively adjust our window size dynamically and believe that there are also optimizations that you could make regarding the round-trip time estimations, potentially accounting for the case that the round trip time may oscillate up and down throughout actual installation. There are also likely optimal values for the default round trip time and growth rate. However, to keep the implementation simple, we kept the round trip time as strictly increasing and maintained a rule of doubling. For the window size, we likely could also optimize having larger window sizes, but decided on a default value of a window size of 8. 

## Contributions

Daniel Yu and Ray Kong
