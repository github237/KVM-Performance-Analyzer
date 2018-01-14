# KVM-Performance-Analyzer-Linux-Kernel
Linux Source Code https://github.com/torvalds/linux

This project is about adding counters into the KVM that track the following information:

    1. Total number of exits (for each type of exit KVM enables)
    2. Max/Min/Average number of CPU cycles for each exit type
    3. Total amount of cycles spent processing all exits

The above information can help us analyze the KVM performance. We first compile the linux kernel and then modify the kvm code in the linux source code directory. Then we insert our compiled module and check the output. We measure two outputs one with Extended Page Table (EPT)/ Nested Page Table (NPT) Enabled and another with EPT/NPT disabled which will force the KVM to use shadow paging. Here we will be using output dump for every 500 VM exits.

[Output (EPT Enabled)](https://github.com/shikhargaur1990/KVM-Performance-Analyzer/blob/master/output1.png)

[Output (EPT Disabled)](https://github.com/shikhargaur1990/KVM-Performance-Analyzer/blob/master/output2.png)

# Steps followed:
    1. Compile your own Linux kernel 
    2. Modify the code in linux/arch/x86/kvm/vmx.c
    3. We modify the exit handler function vmx_handle_exit(struct kvm_vcpu *vcpu) for calculating the stats
    4. Compile the kernel by command: make modules
    5. Remove the current kernel using rmmod for kvm_intel.ko and kvm.ko
    6. Insert the new Kernel using insmod for kvm.ko and kvm_intel.ko
    7. Fire up the VM in kvm
    8. Check the output in dmesg buffer
    9. For EPT disabled output, insert the module using ept=0 and check the output
