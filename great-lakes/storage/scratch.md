---
layout: default
title: /scratch
parent: Storage
grand_parent: Great Lakes
nav_order: 1
---

# `/scratch`

`/scratch` is by far the fastest file system and should be your default choice for most of your work, especially disk I/O heavy work like data preprocessing, data reading, checkpointing, etc. We get 10TB of space per root account, which we have one `chaijy_root`. Note that data not accessed for 60 days will be purged from `/scratch`, which is long enough for most cases.

Our `/scratch` directory is located at `/scratch/chaijy_root`. You can access it via a node on Great Lakes, e.g., your login machine:

```bash
$ ll /scratch/chaijy_root/
total 3
drwxrws--- 31 root chaijy_root 4096 Feb 17 16:10 chaijy0
drwxrws--- 31 root chaijy_root 4096 Apr 14 18:45 chaijy1
drwxrws--- 36 root chaijy_root 4096 Apr 12 21:25 chaijy2
```

You'll notice that we have a sub-directory per Great Lakes account. Each account directory has a directory for each user on that account:

```bash
$ ll /scratch/chaijy_root/chaijy2/
total 34
drwx--S---  2 anishmah chaijy_root 4096 Jun  7  2022 anishmah
drwx--S---  2 bdepst   chaijy_root 4096 Dec  8  2021 bdepst
drwx--S---  2 bensvdp  chaijy_root 4096 Sep  9  2021 bensvdp
drwx--S---  3 cpbara   chaijy_root 4096 Jun 14  2022 cpbara
drwx--S---  2 creiglas chaijy_root 4096 Feb 13 20:03 creiglas
drwx--S---  2 devrajn  chaijy_root 4096 Mar 17  2022 devrajn
drwx--S---  2 haoyiqiu chaijy_root 4096 Dec  6  2021 haoyiqiu
drwx--S---  2 ikhee    chaijy_root 4096 Jan 21  2022 ikhee
drwx--S---  2 jhsansom chaijy_root 4096 Mar 12 18:38 jhsansom
drwx--S---  2 jiahaoq  chaijy_root 4096 Dec  6  2021 jiahaoq
drwx--S---  3 jianingy chaijy_root 4096 Apr 19  2022 jianingy
drwxrws--- 18 jiayipan chaijy_root 4096 Apr 17 19:55 jiayipan
drwxr-sr-x  3 jiayipan chaijy_root 4096 Sep  6  2022 jiayipan-Archive
drwx--S---  2 kpyu     chaijy_root 4096 Feb  1  2022 kpyu
drwx--S---  2 lattimer chaijy_root 4096 May 27  2022 lattimer
drwx--S---  2 luxinyu  chaijy_root 4096 Mar 31  2022 luxinyu
drwx--S---  2 marstin  chaijy_root 4096 Sep  9  2021 marstin
drwx--S---  2 nickhu   chaijy_root 4096 Jan 21  2022 nickhu
drwx--S---  2 oliviaaa chaijy_root 4096 Apr 11  2022 oliviaaa
drwx--S---  2 owenhji  chaijy_root 4096 Feb 15  2022 owenhji
drwx--S---  2 ponyz    chaijy_root 4096 Sep  8  2022 ponyz
drwx--S---  3 qianqi   chaijy_root 4096 May 17  2022 qianqi
drwx--S---  3 roihn    chaijy_root 4096 Mar 28 17:22 roihn
drwx--S---  3 seanpaul chaijy_root 4096 Apr 28  2022 seanpaul
drwxrws---  3 root     chaijy_root 4096 Feb 12  2022 shared_data
drwx--S---  3 sstorks  chaijy_root 4096 Feb 15  2022 sstorks
drwx--S---  2 twenfei  chaijy_root 4096 Feb  1  2022 twenfei
drwx--S---  2 ximic    chaijy_root 4096 Feb  7  2022 ximic
drwx--S---  2 xingyaow chaijy_root 4096 Mar  8  2022 xingyaow
drwx--S---  2 xuweic   chaijy_root 4096 Jun  7  2022 xuweic
drwx--S---  2 yuweibao chaijy_root 4096 Sep  9  2021 yuweibao
drwx--S---  2 zekun    chaijy_root 4096 Mar 12 18:37 zekun
drwx--S---  2 zhangyic chaijy_root 4096 Sep  9  2021 zhangyic
drwx--S---  2 zheyuan  chaijy_root 4096 Jan 30 12:57 zheyuan
```

You can put your data under your user directory. It doesn't really matter which account sub-directory you use, but it's good to keep it the same as the account your Great Lakes job will be run on.
