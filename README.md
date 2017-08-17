## kmod - Linux kernel module handling

[![Build Status](https://semaphoreci.com/api/v1/projects/29d989ba-0f70-4006-be21-550f6692b73b/449920/shields_badge.svg)](https://semaphoreci.com/lucasdemarchi/kmod)<br/>
[![Coverity Scan Status](https://scan.coverity.com/projects/2096/badge.svg)](https://scan.coverity.com/projects/2096)

This is a ***mirror only***. Please see [README](../master/README) file for more information.

Patch depmod with a -d option for displaying debugging output, eg:

```
depmod -dall
...
snd_soc_sst_cht_bsw_rt5645:
    snd_soc_dai_set_tdm_slot            (0x19bf0779) U snd_soc_core 
    snd_pcm_hw_constraint_minmax        (0x46c15d4e) U snd_pcm      
    snd_soc_card_jack_new               (0x539d527e) U snd_soc_core 
    snd_soc_dai_set_sysclk              (0x8bc64e36) U snd_soc_core 
    rt5645_sel_asrc_clk_src             (0xec88097a) U snd_soc_rt5645
    snd_soc_dapm_get_pin_switch         (0xe3a9da25) U snd_soc_core 
    rt5645_set_jack_detect              (0x81bfe739) U snd_soc_rt5645
    snd_soc_dai_set_pll                 (0xd8ba384a) U snd_soc_core 
    snd_soc_dapm_put_pin_switch         (0xf3a69239) U snd_soc_core 
    snd_soc_dapm_info_pin_switch        (0x38295078) U snd_soc_core 
...
```

Which shows the symbols `snd_soc_sst_cht_bsw_rt5645` kernel module depends on, their
CRCs, ELF symbol type (Undefined, Weak, None, Global, Local), and the module which
provides it.

The "builtins" option does the same but does not exclude symbols provided by the
running (or selected) kernel. For these symbols instead of the module name it
prints `uname -r` (or the specified kernel).

The "reverse" option prints the kernel modules, the symbols they export, and which
modules rely on those specific symbols:

```
...
vfio:
    vfio_external_check_extension       (0xc1d989c5) 
    vfio_register_iommu_driver          (0x6d1786a3) vfio_iommu_type1 
    vfio_group_get_external_user        (0x2ab5ee40) vfio_pci 
    vfio_group_put_external_user        (0xc4913442) vfio_pci 
    vfio_external_user_iommu_id         (0x3567743b) vfio_pci 
    vfio_unregister_iommu_driver        (0x57d61bf2) vfio_iommu_type1 
    vfio_device_put                     (0x969c73d9) vfio_pci 
    vfio_add_group_dev                  (0x4f42a81d) vfio_pci 
    vfio_device_data                    (0x95258207) vfio_pci 
    vfio_device_get_from_dev            (0x8f91a3b5) vfio_pci 
    vfio_del_group_dev                  (0xc6d0d39f) vfio_pci 
...
```

