# PS4Offsets & Payloads 1.76/4.05/4.55

<p align="center">
🔥 PS4Offsets ~ Use these offsets if you need to update yuor old payloads. 🔥
  <br>
  
  These Offsets are for 4.55 firmware.
  
``` 
//4.55 KERN
#define	KERN_XFAST_SYSCALL 0x3095D0
#define KERN_PROCESS_ASLR 0x1BA559
#define KERN_PRISON_0 0x10399B0
#define KERN_ROOTVNODE 0x21AFA30
#define KERN_PTRACE_CHECK 0x17D2C1

//Reading 4.55 kernel_base...
void* kernel_base = &((uint8_t*)__readmsr(0xC0000082))[-KERN_XFAST_SYSCALL];
uint8_t* kernel_ptr = (uint8_t*)kernel_base;
void** got_prison0 =   (void**)&kernel_ptr[KERN_PRISON_0];
void** got_rootvnode = (void**)&kernel_ptr[KERN_ROOTVNODE];

// sceSblACMgrIsSystemUcred
uint64_t *sonyCred = (uint64_t *)(((char *)td_ucred) + 96);
*sonyCred = 0xffffffffffffffff;
// sceSblACMgrGetDeviceAccessType
uint64_t *sceProcType = (uint64_t *)(((char *)td_ucred) + 88);
*sceProcType = 0x3801000000000013; // Max access
// sceSblACMgrHasSceProcessCapability
uint64_t *sceProcCap = (uint64_t *)(((char *)td_ucred) + 104);
*sceProcCap = 0xffffffffffffffff; // Sce Process

// debug settings FULL
kernelBase[0x1B6D086] |= 0x14;
kernelBase[0x1B6D0A9] |= 0x3;
kernelBase[0x1B6D0AA] |= 0x1;
kernelBase[0x1B6D0C8] |= 0x1;

// Disable write protection
*(uint32_t*)&kernelBase[0x4D70F7] = 0;
*(uint32_t*)&kernelBase[0x4D7F81] = 0;

//UART Enabler 4.55
*(char *)(kernel_base + 0x1997BC8) = 0;

//EAP Internal Partition Key
kernelBase[0x258CCD0]
```
Please make an pull request for anything that is missing or want to add something.

## Contributors
Massive thanks to the following:

- [qwertyoruiopz](https://twitter.com/qwertyoruiopz)
- [Flatz](https://twitter.com/flat_z)
- Anonymous

- [DarkElement](https://twitter.com/zordon605)
- [Vultra](https://twitter.com/C0rpVultra)
