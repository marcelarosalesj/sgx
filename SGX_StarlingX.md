# SGX on StarlingX
This experiment is based on the [SGX for CentOS guide](https://github.com/marcelarosalesj/sgx-starlingx/blob/master/SGX_CentOS.md). The idea is to reproduce it, but on a StarlingX installation.

_Disclaimer: I couldn't complete the provisioning of an StarlingX system due to lack of hardware. Because of that, this experiment is not using other StarlingX features._

## Steps

1. Install StarlingX

2. Enable SGX on the platform by BIOS.

3. Configure default `ip route`

4. Run ansible playbook. Use a `localhost.yml` if required.

5. Enable access to internet (ie: DNS, proxy)

6. Clone SGX-hardware [1] project to verify if hardware supports SGX.
```
gcc test-sgx.c -o test-sgx
./test-sgx
```

7. Install SGX Linux Driver for CentOS [2].

For this step, you are going to need StarlingX kernel's `kernel-devel` package. You can get it from [CENGN mirror](http://mirror.starlingx.cengn.ca/mirror/).
```
wget http://mirror.starlingx.cengn.ca/mirror/starlingx/master/centos/latest_build/outputs/RPMS/std/kernel-devel-3.10.0-957.21.3.el7.2.tis.x86_64.rpm

sudo rpm -ivh --replacepkgs --replacefiles kernel-devel-3.10.0-957.21.3.el7.2.tis.x86_64.rpm 
```

8. Install SGX SDK and SGX PSW in /opt/intel [3].

9. Go to the SampleCode LocalAttestation
```
$ cd linux-sgx/SampleCode/LocalAttestation
```

10. Generate Local Attestation example in Simulation Mode. This is useful to verify that the installation was successful.
```
$ make SGX_MODE=SIM
$ ./app
```

11. Generate Local Attestation example in Hardware Mode.
```
$ make SGX_MODE=HW
$ ./app
```

## References:
[1] https://github.com/ayeks/SGX-hardware  
[2] https://github.com/intel/linux-sgx-driver  
[3] https://github.com/intel/linux-sgx  
[4] https://github.com/intel/linux-sgx/issues/47  