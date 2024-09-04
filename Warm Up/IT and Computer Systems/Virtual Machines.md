| Course Name  |         Topic         | Professor |     Date      |             Tags              |
| :----------: | :-------------------: | :-------: | :-----------: | :---------------------------: |
| **Clean IT** | Creating a Windows VM | Sebastien | 08 April 2024 | #Windows #ComputerEngineering |

[Class Video Link](https://learn.dsti.institute/mod/url/view.php?id=17651)

# Summary
*A virtual machine allows us to create a partition of our computer's hardware that is completely separate from the host machine. [[Windows|Windows]] provides a software for this called Hyper-V which manages virtual machines and is responsible for the hardware allocation from the host machine.*

# Key Takeaways
1. Hard drive formatting is essential for any [[Operating System|operating system]] to know where to find certain programs like operating systems
	a. In a VM, the memory addresses are reset and translated by the hypervisor
2. If the VM uses dynamic memory, the startup memory is an upper bound but is not all immediately allocated
3. For Windows, the availability of Hyper-V is dependent on your edition
	a. MUST have education, enterprise, or professional edition
4. For most VMs, an operating system will need to be installed upon launching since the hard drive is unformatted

# Definitions
- Hypervisor: A software (not OS specific) that handles the creation and management of virtual machines
	- Windows Hyper-V, VMware, or VMBox as examples
- Non-persistent Environment: An environment/workspace where the resources used while running are not saved for future connections
	- Any data created in a non-persistent environment is destroyed when the environment is spun down

# Additional Resources
- [Windows Virtualization Definition](https://azure.microsoft.com/en-us/resources/cloud-computing-dictionary/what-is-virtualization/?ef_id=_k_Cj0KCQjw2uiwBhCXARIsACMvIU1a4e4VFIlhdIwsJv0d-9pmLzawSocfiNBdliigUFWp2DPKGSAYNi4aAg_CEALw_wcB_k_&OCID=AIDcmme9zx2qiz_SEM__k_Cj0KCQjw2uiwBhCXARIsACMvIU1a4e4VFIlhdIwsJv0d-9pmLzawSocfiNBdliigUFWp2DPKGSAYNi4aAg_CEALw_wcB_k_&gad_source=1&gclid=Cj0KCQjw2uiwBhCXARIsACMvIU1a4e4VFIlhdIwsJv0d-9pmLzawSocfiNBdliigUFWp2DPKGSAYNi4aAg_CEALw_wcB)
- [Windows - What is a Virtual Machine](https://azure.microsoft.com/en-us/resources/cloud-computing-dictionary/what-is-a-virtual-machine)

# Notes
## Hardware Virtualization
- This is a feature that allows a special program called a hypervisor to allocate hardware resources to virtual machines
- Windows provides a non-persistent virtual machine called Windows Sandbox
	- This comes pre-installed with Windows
## Windows Subsystem for Linux (WSL)
- This is also a pre-installed hypervisor that allows for one or multiple [[Linux|linux]] distributions to run natively on the Windows PC
- A Linux kernel must first be installed to use this
	- There are many to choose from that are available in the Windows store
- Of the four well-known Linux kernels, there is one main difference separating them
	- Debian and Ubuntu use the APT package manager
	- Fedora and Red Hat use the YUM package manager
## Connecting to a VM
- The VM waits to find a bootable drive and Operating System
- Initially, we have no OS installed
	- Our hard drive is "unformatted"
- Once we install Windows, we format the hard drive telling the VM where to find the OS
	- Windows requires subsets (partitions) of the dusk to install. The system reserves partitions at 0 and 1, the windows C: drive is then at partition 2




