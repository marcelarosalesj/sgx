# SGX for CentOS

## Steps
1. Enable SGX on the platform by BIOS.
2. Verify Hardware supports SGX [1].
3. Install SGX Linux Driver for CentOS [2].
4. After these steps, you should have up and running the SGX module.
```
$lsmod | grep sgx
isgx
```
5. Install SGX SDK and SGX PSW in /opt/intel [3].
6. Copy SampleCode to home.
```
$ cp -r /opt/intel/sgxsdk/SampleCode ~
```
7. Generate Local Attestation example in Simulation Mode. This is useful to verify that the installation was successful.
```
$ cd ~/SampleCode/LocalAttestation
$ make SGX_MODE=SIM
```
8. Execute the binary.
```
$ ./app
```
9. Generate Local Attestation example in Hardware Mode.
```
$ make SGX_MODE=HW
```
10. Execute the binary.
```
$ ./app
```

## Problems and solutions
* "Please use the correct uRTS library from PSW package" [4]. Solution: Do not set LD_LIBRARY_PATH=/opt/intel/sgxsdk/lib64, link using system folder.

## References:
[1] https://github.com/ayeks/SGX-hardware
[2] https://github.com/intel/linux-sgx-driver
[3] https://github.com/intel/linux-sgx
[4] https://github.com/intel/linux-sgx/issues/47
