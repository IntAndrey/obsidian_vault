Low bandwith speed and high latency when running P2P processes on AS-4125GS-TNRT (H13DSG-O-CPU) with A6000, how can I improve the performance?

Answer

Please disable ASPM, C-State, NUMA, ACS, IOMMU in Bios and install full DIMMs into the system.
Bios> Advanced> PCIe/PCI/PnP Configuration> ASPM Support> Disabled
Bios> Advanced> Global C-State Control> Disabled
Bios> Advanced> ACPI Settings> ACPI SRAT L3 Cache As NUMA Domain
Bios> Advanced> North Bridge(NB) Configuration> ACS Enable> Disabled
Bios> Advanced> North Bridge(NB) Configuration> IOMMU> Disabled