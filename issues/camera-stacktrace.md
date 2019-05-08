# Camera

Using the camera in `cheese` throws a kernel stack trace. It seems to work anyways...
```
[ 2232.508082] ------------[ cut here ]------------
[ 2232.508084] Unknown pixelformat 0x00000000
[ 2232.508118] WARNING: CPU: 1 PID: 8724 at /build/linux-hwe-juiyda/linux-hwe-4.18.0/drivers/media/v4l2-core/v4l2-ioctl.c:1297 v4l_fill_fmtdesc+0xf51/0x12f0 [videodev]
[ 2232.508119] Modules linked in: bluetooth ecdh_generic msr ccm uvcvideo videobuf2_vmalloc videobuf2_memops videobuf2_v4l2 videobuf2_common videodev media snd_hda_codec_hdmi arc4 intel_rapl x86_pkg_temp_thermal intel_powerclamp coretemp kvm_intel nls_iso8859_1 snd_soc_skl kvm iwlmvm snd_soc_skl_ipc irqbypass snd_soc_sst_ipc mac80211 snd_hda_codec_realtek snd_soc_sst_dsp snd_hda_codec_generic intel_cstate snd_hda_ext_core intel_rapl_perf snd_soc_acpi snd_soc_core snd_compress joydev input_leds ac97_bus snd_seq_midi snd_pcm_dmaengine snd_seq_midi_event iwlwifi snd_hda_intel serio_raw snd_rawmidi snd_hda_codec snd_seq snd_hda_core ucsi_acpi thinkpad_acpi mei_me snd_hwdep wmi_bmof intel_wmi_thunderbolt processor_thermal_device typec_ucsi nvram cfg80211 mei intel_pch_thermal intel_soc_dts_iosf typec snd_seq_device
[ 2232.508176]  snd_pcm snd_timer snd int3403_thermal soundcore int340x_thermal_zone int3400_thermal mac_hid acpi_thermal_rel acpi_pad sch_fq_codel parport_pc ppdev lp parport ip_tables x_tables autofs4 btrfs xor zstd_compress raid6_pq libcrc32c algif_skcipher af_alg dm_crypt dm_mirror dm_region_hash dm_log crct10dif_pclmul crc32_pclmul ghash_clmulni_intel i915 pcbc aesni_intel psmouse aes_x86_64 crypto_simd i2c_algo_bit cryptd glue_helper drm_kms_helper syscopyarea sysfillrect sysimgblt fb_sys_fops nvme video drm e1000e pinctrl_cannonlake pinctrl_intel nvme_core wmi
[ 2232.508229] CPU: 1 PID: 8724 Comm: cheese Not tainted 4.18.0-18-generic #19~18.04.1-Ubuntu
[ 2232.508230] Hardware name: LENOVO 20NYS02A00/20NYS02A00, BIOS N2JET29W (1.07 ) 02/19/2019
[ 2232.508239] RIP: 0010:v4l_fill_fmtdesc+0xf51/0x12f0 [videodev]
[ 2232.508240] Code: 53 4f 4e 58 0f 84 5c 02 00 00 3d 64 76 73 64 48 c7 c6 ee 78 c1 c0 0f 84 71 f5 ff ff 89 c6 48 c7 c7 92 7a c1 c0 e8 3f d5 28 e3 <0f> 0b 80 7b 0c 00 0f 85 73 f5 ff ff 8b 43 2c 48 c7 c1 a0 6d c1 c0 
[ 2232.508289] RSP: 0018:ffffb95d820ebc48 EFLAGS: 00010282
[ 2232.508292] RAX: 0000000000000000 RBX: ffffb95d820ebd80 RCX: 0000000000000006
[ 2232.508294] RDX: 0000000000000007 RSI: 0000000000000092 RDI: ffff9e81844564b0
[ 2232.508295] RBP: ffffb95d820ebc58 R08: 000000000000035a R09: 0000000000000004
[ 2232.508297] R10: ffff9e8166e26900 R11: 0000000000000001 R12: ffff9e816f9ade00
[ 2232.508299] R13: ffffffffc0e989a0 R14: ffff9e8166e269c0 R15: ffffffffffffffed
[ 2232.508301] FS:  00007fa89c676700(0000) GS:ffff9e8184440000(0000) knlGS:0000000000000000
[ 2232.508303] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
[ 2232.508305] CR2: 00007fa89400e8a8 CR3: 000000046fada003 CR4: 00000000003606e0
[ 2232.508306] Call Trace:
[ 2232.508317]  v4l_enum_fmt+0x74/0x110 [videodev]
[ 2232.508325]  __video_do_ioctl+0x1ad/0x3c0 [videodev]
[ 2232.508329]  ? path_openat+0x608/0x1780
[ 2232.508333]  ? filename_lookup+0xe0/0x190
[ 2232.508341]  video_usercopy+0x1af/0x670 [videodev]
[ 2232.508348]  ? v4l_fill_fmtdesc+0x12f0/0x12f0 [videodev]
[ 2232.508356]  video_ioctl2+0x15/0x20 [videodev]
[ 2232.508363]  v4l2_ioctl+0x49/0x50 [videodev]
[ 2232.508367]  do_vfs_ioctl+0xa8/0x630
[ 2232.508370]  ? putname+0x4c/0x60
[ 2232.508373]  ksys_ioctl+0x75/0x80
[ 2232.508377]  __x64_sys_ioctl+0x1a/0x20
[ 2232.508382]  do_syscall_64+0x5a/0x120
[ 2232.508387]  entry_SYSCALL_64_after_hwframe+0x44/0xa9
[ 2232.508389] RIP: 0033:0x7fa8c2de15d7
[ 2232.508390] Code: b3 66 90 48 8b 05 b1 48 2d 00 64 c7 00 26 00 00 00 48 c7 c0 ff ff ff ff c3 66 2e 0f 1f 84 00 00 00 00 00 b8 10 00 00 00 0f 05 <48> 3d 01 f0 ff ff 73 01 c3 48 8b 0d 81 48 2d 00 f7 d8 64 89 01 48 
[ 2232.508439] RSP: 002b:00007fa89c675898 EFLAGS: 00000246 ORIG_RAX: 0000000000000010
[ 2232.508442] RAX: ffffffffffffffda RBX: 00007fa89400b850 RCX: 00007fa8c2de15d7
[ 2232.508443] RDX: 00007fa8940143e0 RSI: 00000000c0405602 RDI: 0000000000000013
[ 2232.508445] RBP: 00007fa8c54b2768 R08: 00007fa8940143e0 R09: 0000000000000000
[ 2232.508446] R10: 00007fa8940008d0 R11: 0000000000000246 R12: 0000000000000000
[ 2232.508448] R13: 00007fa894008860 R14: 0000000000000001 R15: 00007fa8940143e0
[ 2232.508450] ---[ end trace 76f312cfce3e57bb ]---
```
