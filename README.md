# optane-dcpmm-proxmox-tests

HPE dl380 single 6230 128GB Rdimm ( 4x 32GB)  +  2X 256 optane DCPMM interleaved in app direct mode


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
