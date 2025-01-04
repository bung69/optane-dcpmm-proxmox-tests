args: -machine nvdimm=on,nvdimm-persistence=mem-ctrl -m slots=3,maxmem=650G -object memory-backend-file,id=mem1,share,mem-path=/mnt/pmem0.4,size=100G,align=128M -device nvdimm,memdev=mem1,id=nv1,label-size=2M -object memory-backend-file,id=mem2,share,mem-path=/dev/dax0.5,size=100G,align=128M -device nvdimm,memdev=mem2,id=nv2,label-size=2M


# optane-dcpmm-proxmox-tests

HPE dl380 single 6230 128GB Rdimm ( 4x 32GB)  +  2X 256 optane DCPMM interleaved in app direct mode

# Latancy optimised bios setting
## Raw namespace with sectorsize 512 and xfs

```
Sequential Read: 2813MB/s IOPS=10
Sequential Write: 3192MB/s IOPS=12

512KB Read: 2983MB/s IOPS=5967
512KB Write: 3636MB/s IOPS=7272

Sequential Q32T1 Read: 2825MB/s IOPS=353
Sequential Q32T1 Write: 3121MB/s IOPS=390

4KB Read: 1239MB/s IOPS=317212
4KB Write: 1028MB/s IOPS=263408

4KB Q32T1 Read: 1267MB/s IOPS=324435
4KB Q32T1 Write: 913MB/s IOPS=233890

4KB Q8T8 Read: 7700MB/s IOPS=1971390
4KB Q8T8 Write: 3931MB/s IOPS=1006347
```

## fdax namespace with sectorsize 512 xfs mounted with dax

```
Sequential Read: 2929MB/s IOPS=11
Sequential Write: 3359MB/s IOPS=13

512KB Read: 3333MB/s IOPS=6666
512KB Write: 3798MB/s IOPS=7596

Sequential Q32T1 Read: 2929MB/s IOPS=366
Sequential Q32T1 Write: 3386MB/s IOPS=423

4KB Read: 1534MB/s IOPS=392901
4KB Write: 1462MB/s IOPS=374491

4KB Q32T1 Read: 1527MB/s IOPS=391026
4KB Q32T1 Write: 1064MB/s IOPS=272385

4KB Q8T8 Read: 9306MB/s IOPS=2382414
4KB Q8T8 Write: 1350MB/s IOPS=345745
```

## fdax namespace with sectorsize 512 xfs mounted with dax 2M aligned
```
--- . (xfs /dev/pmem0.2 147.6 GiB) ioping statistics ---
23 requests completed in 338.2 us, 92 KiB read, 68.0 k iops, 265.6 MiB/s
generated 24 requests in 23.8 s, 96 KiB, 1 iops, 4.04 KiB/s
min/avg/max/mdev = 6.42 us / 14.7 us / 25.7 us / 3.08 us
```

## fdax namespace with sectorsize 4096 xfs mounted with dax

```
  Sequential Read: 2942MB/s IOPS=11
  Sequential Write: 3368MB/s IOPS=13
  
  512KB Read: 3324MB/s IOPS=6649
  512KB Write: 3867MB/s IOPS=7734
  
  Sequential Q32T1 Read: 2935MB/s IOPS=366
  Sequential Q32T1 Write: 3350MB/s IOPS=418
  
  4KB Read: 1551MB/s IOPS=397187
  4KB Write: 1330MB/s IOPS=340623
  
  4KB Q32T1 Read: 1520MB/s IOPS=389168
  4KB Q32T1 Write: 1066MB/s IOPS=273066
  
  4KB Q8T8 Read: 9392MB/s IOPS=2404471
  4KB Q8T8 Write: 1341MB/s IOPS=343508
```


## fdax namespace passed to fedora VM with Dax mount
```
Sequential Read: 548MB/s IOPS=4
Sequential Write: 219MB/s IOPS=1

512KB Read: 891MB/s IOPS=1782
512KB Write: 217MB/s IOPS=434

Sequential Q32T1 Read: 1178MB/s IOPS=294
Sequential Q32T1 Write: 222MB/s IOPS=55

4KB Read: 79MB/s IOPS=20467
4KB Write: 84MB/s IOPS=21504

4KB Q32T1 Read: 230MB/s IOPS=58977
4KB Q32T1 Write: 149MB/s IOPS=38235

4KB Q8T8 Read: 697MB/s IOPS=178685
4KB Q8T8 Write: 174MB/s IOPS=44784


```

## fdax namespace passed to fedora VM with Dax mount 2M aligned

```
Sequential Read: 2723MB/s IOPS=10
Sequential Write: 3192MB/s IOPS=12

512KB Read: 3820MB/s IOPS=7641
512KB Write: 3565MB/s IOPS=7130

Sequential Q32T1 Read: 2770MB/s IOPS=346
Sequential Q32T1 Write: 3176MB/s IOPS=397

4KB Read: 1534MB/s IOPS=392901
4KB Write: 1348MB/s IOPS=345289

4KB Q32T1 Read: 1557MB/s IOPS=398637
4KB Q32T1 Write: 975MB/s IOPS=249756

4KB Q8T8 Read: 9433MB/s IOPS=2414965
4KB Q8T8 Write: 1268MB/s IOPS=324658
```
## fdax namespace passed to Rocky VM with Dax mount 2M aligned
```
--- . (xfs /dev/pmem0 98.2 GiB) ioping statistics ---
23 requests completed in 415.8 us, 92 KiB read, 55.3 k iops, 216.1 MiB/s
generated 24 requests in 23.9 s, 96 KiB, 1 iops, 4.02 KiB/s
min/avg/max/mdev = 7.88 us / 18.1 us / 28.3 us / 5.93 us
```


## devdax namespace passed to fedora VM with Dax mount 2M aligned
```
Sequential Read: 2869MB/s IOPS=11
Sequential Write: 3224MB/s IOPS=12

512KB Read: 3798MB/s IOPS=7596
512KB Write: 3595MB/s IOPS=7191

Sequential Q32T1 Read: 2949MB/s IOPS=368
Sequential Q32T1 Write: 3240MB/s IOPS=405

4KB Read: 1559MB/s IOPS=399123
4KB Write: 1551MB/s IOPS=397187

4KB Q32T1 Read: 1568MB/s IOPS=401568
4KB Q32T1 Write: 1012MB/s IOPS=259240

4KB Q8T8 Read: 9366MB/s IOPS=2397834
4KB Q8T8 Write: 1326MB/s IOPS=339499
```

## devdax namespace passed to Rocky VM with sector namespace.  rocky installed on root with EFI and boot on qemu disk
```
Sequential Read: 2869MB/s IOPS=11
Sequential Write: 925MB/s IOPS=3

512KB Read: 2863MB/s IOPS=5727
512KB Write: 930MB/s IOPS=1861

Sequential Q32T1 Read: 2929MB/s IOPS=366
Sequential Q32T1 Write: 928MB/s IOPS=116

4KB Read: 1025MB/s IOPS=262564
4KB Write: 663MB/s IOPS=169870

4KB Q32T1 Read: 1207MB/s IOPS=309132
4KB Q32T1 Write: 655MB/s IOPS=167782

4KB Q8T8 Read: 7107MB/s IOPS=1819621
4KB Q8T8 Write: 3130MB/s IOPS=801293
```

```
--- . (xfs /dev/pmem1s1 49.7 GiB) ioping statistics ---
28 requests completed in 2.03 ms, 112 KiB read, 13.8 k iops, 53.8 MiB/s
generated 29 requests in 28.6 s, 116 KiB, 1 iops, 4.05 KiB/s
min/avg/max/mdev = 30.6 us / 72.6 us / 89.5 us / 16.8 us
```

# Bandwidth optimised bios setting
## fdax namespace with sectorsize 512 xfs mounted with dax 2M aligned

```
256m Sequential Read: 1344MB/s IOPS=5
256m Sequential Write: 5493MB/s IOPS=21

512KB Read: 8258MB/s IOPS=16516
512KB Write: 10240MB/s IOPS=20480

8m Sequential Q32T1 Read: 5355MB/s IOPS=669
8m Sequential Q32T1 Write: 6037MB/s IOPS=754

4KB Read: 1212MB/s IOPS=310303
4KB Write: 777MB/s IOPS=199076

4KB Q32T1 Read: 1430MB/s IOPS=366122
4KB Q32T1 Write: 784MB/s IOPS=200907

4KB Q8T8 Read: 3852MB/s IOPS=986201
4KB Q8T8 Write: 1691MB/s IOPS=432994
```
# latancy optimised bios setting
## windows 11 bare metal crystal disk mark

```
[Read]
  SEQ    1MiB (Q=  1, T= 1):  3682.776 MB/s [   3512.2 IOPS] <   284.31 us>
  RND    4KiB (Q=  1, T= 1):  1294.470 MB/s [ 316032.7 IOPS] <     3.03 us>

[Write]
  SEQ    1MiB (Q=  1, T= 1):  1277.165 MB/s [   1218.0 IOPS] <   820.20 us>
  RND    4KiB (Q=  1, T= 1):   601.285 MB/s [ 146798.1 IOPS] <     6.65 us>
```

## bb recomeneded -  disabled c states, Ubuntu VM 2 vcpu, 4 cpu affinity for vcpu and io threads, virtio single io thread etc.
```
device: (g=0): rw=read, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=libaio, iodepth=1
fio-3.36
Starting 1 process
Jobs: 1 (f=1): [R(1)][100.0%][r=139MiB/s][r=35.6k IOPS][eta 00m:00s]
device: (groupid=0, jobs=1): err= 0: pid=3142: Sat Jan  4 22:49:58 2025
  read: IOPS=35.5k, BW=139MiB/s (145MB/s)(8324MiB/60001msec)
    slat (nsec): min=4562, max=110646, avg=5841.38, stdev=802.26
    clat (nsec): min=889, max=2492.6k, avg=21643.42, stdev=11927.76
     lat (usec): min=17, max=2498, avg=27.48, stdev=11.93
    clat percentiles (usec):
     |  1.00th=[   19],  5.00th=[   21], 10.00th=[   21], 20.00th=[   21],
     | 30.00th=[   22], 40.00th=[   22], 50.00th=[   22], 60.00th=[   22],
     | 70.00th=[   22], 80.00th=[   23], 90.00th=[   23], 95.00th=[   23],
     | 99.00th=[   27], 99.50th=[   29], 99.90th=[   31], 99.95th=[   32],
     | 99.99th=[  105]
   bw (  KiB/s): min=139448, max=147968, per=100.00%, avg=142099.52, stdev=2074.88, samples=120
   iops        : min=34862, max=36992, avg=35524.83, stdev=518.71, samples=120
  lat (nsec)   : 1000=0.01%
  lat (usec)   : 2=0.01%, 4=0.04%, 10=0.23%, 20=3.46%, 50=96.25%
  lat (usec)   : 100=0.01%, 250=0.01%, 500=0.01%, 750=0.01%, 1000=0.01%
  lat (msec)   : 2=0.01%, 4=0.01%
  cpu          : usr=10.11%, sys=39.67%, ctx=2129541, majf=0, minf=36
  IO depths    : 1=100.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=2131021,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
   READ: bw=139MiB/s (145MB/s), 139MiB/s-139MiB/s (145MB/s-145MB/s), io=8324MiB (8729MB), run=60001-60001msec

Disk stats (read/write):
  sdb: ios=3197327/0, sectors=25578616/0, merge=0/0, ticks=63896/0, in_queue=63896, util=48.72%
```

