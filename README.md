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
# as above without ip thread and cpu affinity
```
device: (g=0): rw=read, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=libaio, iodepth=1
fio-3.36
Starting 1 process
Jobs: 1 (f=1): [R(1)][100.0%][r=85.8MiB/s][r=22.0k IOPS][eta 00m:00s]
device: (groupid=0, jobs=1): err= 0: pid=2592: Sat Jan  4 23:55:06 2025
  read: IOPS=24.1k, BW=94.3MiB/s (98.8MB/s)(5655MiB/60001msec)
    slat (usec): min=4, max=1391, avg= 6.59, stdev= 2.17
    clat (nsec): min=1009, max=3482.9k, avg=34186.92, stdev=20457.36
     lat (usec): min=22, max=3488, avg=40.78, stdev=20.67
    clat percentiles (usec):
     |  1.00th=[   28],  5.00th=[   30], 10.00th=[   30], 20.00th=[   31],
     | 30.00th=[   31], 40.00th=[   35], 50.00th=[   35], 60.00th=[   36],
     | 70.00th=[   36], 80.00th=[   37], 90.00th=[   39], 95.00th=[   39],
     | 99.00th=[   42], 99.50th=[   44], 99.90th=[   50], 99.95th=[   95],
     | 99.99th=[ 1156]
   bw (  KiB/s): min=82144, max=111440, per=100.00%, avg=96543.12, stdev=8548.87, samples=120
   iops        : min=20536, max=27860, avg=24135.72, stdev=2137.22, samples=120
  lat (usec)   : 2=0.01%, 4=0.01%, 10=0.01%, 20=0.01%, 50=99.89%
  lat (usec)   : 100=0.05%, 250=0.02%, 500=0.01%, 750=0.01%, 1000=0.01%
  lat (msec)   : 2=0.01%, 4=0.01%
  cpu          : usr=6.34%, sys=29.91%, ctx=1447782, majf=0, minf=36
  IO depths    : 1=100.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=1447790,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
   READ: bw=94.3MiB/s (98.8MB/s), 94.3MiB/s-94.3MiB/s (98.8MB/s-98.8MB/s), io=5655MiB (5930MB), run=60001-60001msec

Disk stats (read/write):
  sdb: ios=2178331/0, sectors=17426648/0, merge=0/0, ticks=71586/0, in_queue=71586, util=65.64%

```

## disabled c states, Ubuntu VM 2 vcpu, 4 cpu affinity for vcpu and io threads, virtio blk io thread etc.
```
device: (g=0): rw=read, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=libaio, iodepth=1
fio-3.36
Starting 1 process
Jobs: 1 (f=1): [R(1)][100.0%][r=232MiB/s][r=59.4k IOPS][eta 00m:00s]
device: (groupid=0, jobs=1): err= 0: pid=2627: Sat Jan  4 23:00:59 2025
  read: IOPS=58.7k, BW=229MiB/s (241MB/s)(13.4GiB/60001msec)
    slat (nsec): min=1744, max=3400.8k, avg=2519.23, stdev=6119.87
    clat (nsec): min=734, max=5536.2k, avg=13970.67, stdev=14927.97
     lat (usec): min=10, max=5539, avg=16.49, stdev=16.13
    clat percentiles (nsec):
     |  1.00th=[12480],  5.00th=[12608], 10.00th=[12736], 20.00th=[13504],
     | 30.00th=[13632], 40.00th=[13760], 50.00th=[13760], 60.00th=[13888],
     | 70.00th=[14016], 80.00th=[14272], 90.00th=[14528], 95.00th=[14784],
     | 99.00th=[18304], 99.50th=[19584], 99.90th=[21888], 99.95th=[23424],
     | 99.99th=[38144]
   bw (  KiB/s): min=228697, max=245346, per=100.00%, avg=235002.41, stdev=4729.84, samples=120
   iops        : min=57174, max=61336, avg=58750.57, stdev=1182.51, samples=120
  lat (nsec)   : 750=0.01%, 1000=0.06%
  lat (usec)   : 2=0.01%, 4=0.01%, 10=0.02%, 20=99.48%, 50=0.43%
  lat (usec)   : 100=0.01%, 250=0.01%, 500=0.01%, 750=0.01%, 1000=0.01%
  lat (msec)   : 2=0.01%, 4=0.01%, 10=0.01%
  cpu          : usr=15.66%, sys=43.16%, ctx=3520201, majf=0, minf=36
  IO depths    : 1=100.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=3524234,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
   READ: bw=229MiB/s (241MB/s), 229MiB/s-229MiB/s (241MB/s-241MB/s), io=13.4GiB (14.4GB), run=60001-60001msec

Disk stats (read/write):
  vda: ios=5255629/0, sectors=42045032/0, merge=0/0, ticks=50205/0, in_queue=50205, util=40.03%
```
# as above without io thread and cpu affinity

```
device: (g=0): rw=read, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=libaio, iodepth=1
fio-3.36
Starting 1 process
Jobs: 1 (f=1): [R(1)][100.0%][r=120MiB/s][r=30.8k IOPS][eta 00m:00s]
device: (groupid=0, jobs=1): err= 0: pid=2568: Sat Jan  4 23:49:15 2025
  read: IOPS=31.3k, BW=122MiB/s (128MB/s)(7339MiB/60001msec)
    slat (usec): min=3, max=5402, avg= 4.67, stdev= 7.35
    clat (nsec): min=824, max=5745.7k, avg=26612.64, stdev=32743.38
     lat (usec): min=16, max=5750, avg=31.28, stdev=33.57
    clat percentiles (usec):
     |  1.00th=[   24],  5.00th=[   25], 10.00th=[   25], 20.00th=[   26],
     | 30.00th=[   26], 40.00th=[   26], 50.00th=[   26], 60.00th=[   26],
     | 70.00th=[   27], 80.00th=[   27], 90.00th=[   28], 95.00th=[   29],
     | 99.00th=[   33], 99.50th=[   35], 99.90th=[   67], 99.95th=[  318],
     | 99.99th=[ 1827]
   bw (  KiB/s): min=63126, max=129856, per=100.00%, avg=125258.93, stdev=7780.56, samples=119
   iops        : min=15781, max=32464, avg=31314.71, stdev=1945.20, samples=119
  lat (nsec)   : 1000=0.01%
  lat (usec)   : 2=0.01%, 4=0.01%, 10=0.01%, 20=0.36%, 50=99.50%
  lat (usec)   : 100=0.04%, 250=0.02%, 500=0.02%, 750=0.01%, 1000=0.01%
  lat (msec)   : 2=0.02%, 4=0.01%, 10=0.01%
  cpu          : usr=8.58%, sys=31.94%, ctx=1878910, majf=0, minf=36
  IO depths    : 1=100.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=1878825,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
   READ: bw=122MiB/s (128MB/s), 122MiB/s-122MiB/s (128MB/s-128MB/s), io=7339MiB (7696MB), run=60001-60001msec

Disk stats (read/write):
  vda: ios=2814964/0, sectors=22519712/0, merge=0/0, ticks=65280/0, in_queue=65280, util=49.91%
```
## disabled c states, Ubuntu VM 2 vcpu, 4 cpu affinity for vcpu and io threads, virtio blk io thread + haltpoll default
```
device: (g=0): rw=read, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=libaio, iodepth=1
fio-3.36
Starting 1 process
Jobs: 1 (f=1): [R(1)][100.0%][r=304MiB/s][r=77.9k IOPS][eta 00m:00s]
device: (groupid=0, jobs=1): err= 0: pid=2973: Sun Jan  5 00:54:41 2025
  read: IOPS=78.0k, BW=305MiB/s (319MB/s)(17.8GiB/60001msec)
    slat (nsec): min=1765, max=392630, avg=2193.85, stdev=440.78
    clat (nsec): min=693, max=2471.4k, avg=10153.30, stdev=8049.12
     lat (usec): min=9, max=2473, avg=12.35, stdev= 8.06
    clat percentiles (nsec):
     |  1.00th=[ 9792],  5.00th=[ 9792], 10.00th=[ 9920], 20.00th=[ 9920],
     | 30.00th=[ 9920], 40.00th=[10048], 50.00th=[10048], 60.00th=[10048],
     | 70.00th=[10048], 80.00th=[10176], 90.00th=[10176], 95.00th=[10304],
     | 99.00th=[14016], 99.50th=[14912], 99.90th=[16064], 99.95th=[17792],
     | 99.99th=[44288]
   bw (  KiB/s): min=304336, max=317474, per=100.00%, avg=311942.32, stdev=2327.38, samples=120
   iops        : min=76084, max=79368, avg=77985.60, stdev=581.91, samples=120
  lat (nsec)   : 750=0.01%, 1000=0.04%
  lat (usec)   : 2=0.01%, 4=0.01%, 10=40.85%, 20=59.07%, 50=0.02%
  lat (usec)   : 100=0.01%, 250=0.01%, 500=0.01%, 750=0.01%, 1000=0.01%
  lat (msec)   : 2=0.01%, 4=0.01%
  cpu          : usr=15.75%, sys=41.36%, ctx=4673156, majf=0, minf=36
  IO depths    : 1=100.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=4678071,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
   READ: bw=305MiB/s (319MB/s), 305MiB/s-305MiB/s (319MB/s-319MB/s), io=17.8GiB (19.2GB), run=60001-60001msec

Disk stats (read/write):
  vda: ios=6999846/0, sectors=55998776/0, merge=0/0, ticks=55334/0, in_queue=55334, util=46.54%

```


## proxmox host with bb script

```
device: (g=0): rw=read, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=libaio, iodepth=1
fio-3.33
Starting 1 process
Jobs: 1 (f=1): [R(1)][100.0%][r=1309MiB/s][r=335k IOPS][eta 00m:00s]
device: (groupid=0, jobs=1): err= 0: pid=325768: Sat Jan  4 23:06:42 2025
  read: IOPS=334k, BW=1304MiB/s (1367MB/s)(76.4GiB/60001msec)
    slat (nsec): min=1815, max=75020, avg=2286.40, stdev=278.31
    clat (nsec): min=435, max=75061, avg=471.22, stdev=109.86
     lat (nsec): min=2294, max=77305, avg=2757.62, stdev=301.33
    clat percentiles (nsec):
     |  1.00th=[  450],  5.00th=[  454], 10.00th=[  454], 20.00th=[  458],
     | 30.00th=[  458], 40.00th=[  458], 50.00th=[  462], 60.00th=[  462],
     | 70.00th=[  466], 80.00th=[  466], 90.00th=[  532], 95.00th=[  540],
     | 99.00th=[  548], 99.50th=[  548], 99.90th=[  604], 99.95th=[  788],
     | 99.99th=[ 4080]
   bw (  MiB/s): min= 1281, max= 1323, per=100.00%, avg=1304.35, stdev= 8.46, samples=120
   iops        : min=328152, max=338768, avg=333913.47, stdev=2166.44, samples=120
  lat (nsec)   : 500=87.09%, 750=12.85%, 1000=0.01%
  lat (usec)   : 2=0.01%, 4=0.03%, 10=0.01%, 20=0.01%, 50=0.01%
  lat (usec)   : 100=0.01%
  cpu          : usr=20.17%, sys=79.82%, ctx=284, majf=1, minf=37
  IO depths    : 1=100.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=20031947,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
   READ: bw=1304MiB/s (1367MB/s), 1304MiB/s-1304MiB/s (1367MB/s-1367MB/s), io=76.4GiB (82.1GB), run=60001-60001msec

Disk stats (read/write):
  pmem0: ios=0/0, merge=0/0, ticks=0/0, in_queue=0, util=0.00%
```
