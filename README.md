# PC-SPRINT

## Navigating This Document

This README has become somewhat unwieldy, so here's an index.

- [Introduction to PC-SPRINT](#introduction-to-pc-sprint) - A quick introduction to the device and how it works.
- [Original File Listing](#original-file-listing) - The original design and accompanying files as released by Doug Severson in 1985.
- [Retro Canada KiCAD Files](#retro-canada-kicad-files) - KiCAD and gerber files drawn up by [VCFed Forum](http://www.vcfed.org/forum/forum.php) user "Retro Canada" for PCB fabrication.
- [My Own "Retro Canada" Board](#my-own-retro-canada-board) - I had a PCB fabricated and assembled it using the above files.
  - [My Testing](#my-testing) - Notes from my own tests with this board.
  - [My Benchmarks](#my-benchmarks) - Benchmarking results.
    - [Landmark](#landmark) - Results from the Landmark benchmarking tool. 
	- [TOPBENCH](#topbench) - Results from the TOPBENCH benchmarking tool.
	- [CheckIt](#checkit) - Results from the CheckIt diagnostic / benchmarking tool.
	- [MIPS](#mips) - You guessed it. Results from the MIPS benchmarking tool.
	- [Benchmarking Conclusions](#benchmarking-conclusions) - Conclusions on benchmark results.
- [PC-SPRINT v2](#pc-sprint-v2) - My attempt at an improved design.
- [License](#license) - Licensing information for this project and documentation.

## Introduction to PC-SPRINT

The PC-SPRINT is a DIY PC accelerator board design released by Doug Severson in 1985 and given away for free in computer magazines and on BBSes of the time. It is designed to allow overclocking of an [Intel 8088](Datasheets/Intel%208088%20Datasheet.pdf)-based computer such as the IBM 5150 / 5155 / 5160 PCs, PCjr, Tandy 1000, Compaq Portable, and I'm sure a whole lot more.

![My PC-SPRINT Installed In My IBM 5150](Retro%20Canada/Images/Mine/pc-sprint-installed.jpg)

In these machines and other contemporary "PC Compatibles" the system clock is usually generated by a 14.318MHz crystal connected to an [Intel 8284A](Datasheets/Intel%208284A-1%20Datasheet.pdf) Clock Generator Driver. The 8284A divides the crystal's signal by 3 giving us our 4.77MHz clock. Unfortunately we can't just replace the crystal on the motherboard as this would play havoc with all sorts of things. The basis of this accelerator is to provide an additional, faster crystal coupled with an additional 8284A to generate a faster clock signal that will be used exclusively by the CPU.

The PC-SPRINT also adds a "Turbo" switch as found on later PCs to enable / disable the higher clock rate and a hardware reset button, which is lacking on the IBM 5150. The included [WARMBOOT.COM](WARMBOOT.COM) utility sets a BIOS flag which skips the RAM test on a warm boot, making the reset very fast even at stock speed.

When the PC-SPRINT is built with the designer's recommended 22.11MHz crystal the CPU will run at a clock speed of 7.37MHz giving an impressive 64% processing speed increase (on paper). Faster speeds may be possible with faster crystals but were not recommended for stability reasons. Note that in order to utilise this accelerator the original 4.77MHz 8088 CPU must be replaced with either a faster version of the same CPU (e.g. 8088-2) or equivalent clone (e.g. [NEC V20](https://en.wikipedia.org/wiki/NEC_V20), which is highly recommended as it brings other benefits).

Much more information is available in the [original documentation](PCSPRINT.DOC) ([PDF](PCSPRINT.DOC.PDF)).

## Original File Listing

Here is a rough index of the files included with the package as originally distributed:

- [1STREAD.ME](1STREAD.ME) - Listing of project files (you're reading a modern adaptation of this)
- [ARTWRK1X.BOT](ARTWRK1X.BOT) - Bottom layer printed circuit artwork 1x size (obsolete printer format) ([PDF](ARTWRK1X.BOT.PDF))
- [ARTWRK1X.TOP](ARTWRK1X.TOP) - Top layer printed circuit artwork 1x size (obsolete printer format) ([PDF](ARTWRK1X.TOP.PDF))
- [ARTWRK2X.BOT](ARTWRK2X.BOT) - Bottom layer printed circuit artwork 2x size (obsolete printer format) ([PDF](ARTWRK2X.BOT.PDF))
- [ARTWRK2X.TOP](ARTWRK2X.TOP) - Top layer printed circuit artwork 2x size (obsolete printer format) ([PDF](ARTWRK2X.TOP.PDF))
- [FEEDTHRU](FEEDTHRU) - Top - bottom "feed through" connection diagram ([PDF](FEEDTHRU.PDF))
- [NOPRTYCK.COM](NOPRTYCHK.COM) - Program to disable parity checks
- [PARTLIST](PARTLIST) - Parts list & placement drawing ([PDF](PARTLIST.PDF))
- [PCSPRINT.BAT](PCSPRINT.BAT) - Batch file to print PC-SPRINT info & drawings 
- **[PCSPRINT.DOC](PCSPRINT.DOC) - Description & construction info ([PDF](PCSPRINT.DOC.PDF))**
- [SCHEMATC](SCHEMATC) - Electronic circuit diagram ([PDF](SCHEMATC.PDF))
- [WARMBOOT.COM](WARMBOOT.COM) - Program to set "warm boot" flag

Note that some files have PDF conversions which were included with the version of the package as received by myself, so I have also linked those above.

The author was keen to include the original unmodified package of files with future revisions, so it is available in [pcsprint_1985.zip](References/pcsprint_1985.zip).

## Retro Canada KiCAD Files

![3D Render of Retro Canada's PC-SPRINT](Retro%20Canada/Images/render.png)

A Vintage Computer Federation forum user by the name of Retro Canada [redrew the original PCB design in KiCAD](http://www.vcfed.org/forum/showthread.php?60803-I-overclocked-my-IBM-5150) and [released the files freely](https://sites.google.com/site/tandycocoloco/dropbox/PC-SPRINT.zip) on November 26th 2017.

I have added a mirror of this KiCAD project [here](Retro%20Canada/PC-SPRINT.zip). The package includes gerber files so KiCAD is not required if you are planning on sending the files directly to a PCB fabricator.

![Retro Canada's PC-SPRINT](Retro%20Canada/Images/pc-sprint1.jpg)

The user built their own based on these files (pictured above - [more of their pictures here](Retro%20Canada/Images)) but could only get it to run reliably up to a 17.43MHz crystal (CPU clock speed 5.81MHz). It is believed that this is related to DMA activity and/or RAM speed, however without the rest of their system specs it's hard to be sure.

### My Own "Retro Canada" Board

![My PC-SPRINT Built Using Retro Canada's Gerber Files](Retro%20Canada/Images/Mine/pc-sprint-pcb.jpg)

I also successfully built and tested a PC-SPRINT using Retro Canada's files. I used [PCBWay](https://www.pcbway.com/) for my PCB fabrication. Mine has a 21.47727MHz crystal giving a CPU clock speed of 7.16MHz - the same as the popular [Tandy 1000 EX and HX](https://en.wikipedia.org/wiki/Tandy_1000#Tandy_1000_EX_and_HX) machines. Thankfully after extensive testing I haven't run into any of the issues experienced by Retro Canada, even at this higher speed. I'm yet to experiment with a faster crystal but when I do you'll be the first to know.

#### My Testing

Here are the specs of my IBM 5150 as tested:

|Part|Model|Notes|
|---|---|---|
|CPU|[NEC V20](https://en.wikipedia.org/wiki/NEC_V20)|4.77MHz stock / 7.16MHz "turbo" with PC-SPRINT|
|FPU|[Intel 8087-2](https://en.wikipedia.org/wiki/Intel_8087)|8087 co-processor rated up to 8MHz|
|RAM|640KB|(256KB onboard, 384KB on SixPakPlus card)<sup>*</sup>|
|Motherboard|64-256KB [Later Revision](http://www.minuszerodegrees.net/5150/motherboard/5150_motherboard_revisions.htm)|[10/27/82 BIOS](http://minuszerodegrees.net/5150/bios/5150_bios_revisions.htm)|
|HDD|XT-IDE with 512MB CompactFlash card|Running [IDE_XTP.BIN BIOS](https://www.lo-tech.co.uk/wiki/XTIDE_Universal_BIOS)|
|Graphics|IBM CGA||
|Network|3com EtherLink II||
|Floppy|2x Tandon 360KB 5.25"|Stock IBM Floppy ISA interface|
|PSU|Standard 110VAC / 63.5W|
|Operating System|[IBM PC DOS 2000](https://winworldpc.com/product/pc-dos/2000)||

<sup>\* All RAM chips were recently replaced with "New Old Stock" [Samsung KM4164B-15](http://www.minuszerodegrees.net/memory/4164.htm) parts, which have a 150ns access time.</sup>

I have done extensive testing with the above system and had no problems whatsoever. I was expecting issues with DMA activity as others have reported, however have seen none at all. Perhaps this is due to the XT-IDE and its [unusual handling of DMA](https://www.lo-tech.co.uk/xt-cfv3-dma-transfer-mode/). The PC even boots up fine with the turbo mode engaged. Incidentally, cold boot time is 1:02 stock vs. 43 seconds in turbo mode.

The included NOPRTYCHK and WARMBOOT utilities work exactly as advertised with no issues as does the new reset button.

Incidentally, this is how I installed the turbo and reset buttons in the case. Both are 12mm panel mount push buttons - the turbo button is a latching version:

![My PC-SPRINT Reset and Turbo Buttons](Retro%20Canada/Images/Mine/pc-sprint-buttons.jpg)

### My Benchmarks

I ran through a series of benchmarking applications in both turbo and non-turbo mode.

These screenshots (and the videos on [my YouTube channel](https://www.youtube.com/ctrlaltrees)) were captured with a rather elaborate capture setup involving a [CGA2RGB](https://gglabs.us/node/2063), [OSSC](https://videogameperfection.com/products/open-source-scan-converter/) and a [StarTech USB3HDCAP](https://www.startech.com/uk/AV/Converters/Video/usb-3-0-video-capture-device-hdmi-dvi-vga~USB3HDCAP), but that's a tale for another time.

These benchmarks compare the performance of the NEC V20 CPU in stock 4.77MHz and turbo 7.16MHz modes using the PC-SPRINT. Unfortunately I don't have the original Intel 8088 CPU anymore to be able to test, however for some indication of how this system performs compared to a stock 5150 take a look at the [MIPS](#mips) benchmark below.

With the exception of CheckIt, all of these benchmarking tools were downloaded from the [TOPBENCH Other Benchmarks](https://dosbenchmark.wordpress.com/otherbenchmarks/) page.

#### Landmark

Landmark System Speed Test was released in 1984 by Landmark Research Internation Corporation and was one of the first DOS benchmarking tools. Here I'm using version 6.00, the final release from 1993.

![Landmark Benchmark Before And After Results](Retro%20Canada/Images/Mine/Benchmarks/landmark-before-after.jpg)

|Benchmark|V20 Stock|V20 Turbo|Improvement|
|---|---|---|---|
|CPU<sup>*</sup>|3.02MHz|4.60MHz|52.32%|
|FPU|4.56MHz|6.92MHZ|51.75%|
|Video|412.35 chr/ms|446.03 chr/ms|8.17%|

<sup>\* The way this figure is calculated is interesting (and generally considered wrong) but the percentage increase is all that matters to us. There is more information on the way Landmark arrives at their CPU figure [here](https://dosbenchmark.wordpress.com/research/landmark/).

#### TOPBENCH

[TOPBENCH](https://dosbenchmark.wordpress.com/) is a modern realtime DOS benchmarking tool. An interesting feature is its "database", which allows you to compare your system's performance to that submitted by other users. I'm using version 0.38 with the full database.

![TOPBENCH Benchmark Before And After Results](Retro%20Canada/Images/Mine/Benchmarks/topbench-before-after.jpg)

Note that TOPBENCH reports the run times of its tests in microseconds, so a lower score is better (faster).

|Benchmark|V20 Stock|V20 Turbo|Improvement|
|---|---|---|---|
|TOPBENCH Score|5|7|2|
|MemTest|2488μ|1640μ|51.71%|
|MemEA|1863μ|1211μ|53.84%|
|Opcodes|1519μ|991μ|53.28%|
|VidMem|2009μ|1840μ|9.18%|
|3DGames|1408μ|919μ|53.21%|
|Total|9287μ|6601μ|40.69%|

According to the database we've gone from an NCR PC4 to an Olivetti PC-1. As I'm not familiar with either of these machines I guess I'll just have to take their word for it. ;)

#### CheckIt

From [WinWorldPC](https://winworldpc.com/product/checkit/30), who said it better than I ever could:

CheckIt, from TouchStone Software Corporation, is a diagnostic tool for generic PC/XT/AT compatible computers. It can perform tests on RAM, hard disks, video cards, floppy disks, motherboard resources, and I/O devices. It has an easy to use menu interface but can also run tests non-interactively.

I'm running version 3, the last release from 1990. In each of these screenshots the "Stock" value (top grey line) is the (NEC V20) value measured with turbo mode off.

![CheckIt CPU Benchmark Before And After Results](Retro%20Canada/Images/Mine/Benchmarks/checkit-main-system-before-after.jpg)

|Benchmark|V20 Stock|V20 Turbo|Improvement|
|---|---|---|---|
|CPU [Dhrystones](https://en.wikipedia.org/wiki/Dhrystone)|387|597|54.26%|
|FPU [Whetstones](https://en.wikipedia.org/wiki/Whetstone_(benchmark))|123.1K|186K|51.1%|

![CheckIt Hard Disk Benchmark Before And After Results](Retro%20Canada/Images/Mine/Benchmarks/checkit-hard-disk-before-after.jpg)

|Benchmark|V20 Stock|V20 Turbo|Improvement|
|---|---|---|---|
|Transfer Speed|198.9K/sec|303.2K/sec|52.44%|
|Average Seek Time<sup>*</sup>|1.7ms|1.1ms|54.55%|
|Track Seek Time<sup>*</sup>|1.7ms|1.1ms|54.55%|

<sup>\* Note that when it comes to seek times, lower numbers are better.</sup>

![CheckIt Video System Benchmark Before And After Results](Retro%20Canada/Images/Mine/Benchmarks/checkit-video-system-before-after.jpg)

|Benchmark|V20 Stock|V20 Turbo|Improvement|
|---|---|---|---|
|BIOS Video Speed|637chr/sec|968chr/sec|51.96%|
|Direct Video Speed|4837chr/sec|7395chr/sec|52.88%|

![CheckIt RAM Test Results - Turbo Mode](Retro%20Canada/Images/Mine/Benchmarks/checkit-ram-test-turbo-mode.jpg)

I also ran various RAM tests with turbo enabled to see if it would pick up any errors, but all tests passed with no problems.

#### MIPS

Chips & Technologies MIPS was written by Jim Bracking and released in 1986. It's a very comprehensive test covering various number-crunching operations, and even shows your score compared to typical examples of machines of that era - an IBM PC, PC/AT and a Compaq 386.

![MIPS Benchmark Before And After Results](Retro%20Canada/Images/Mine/Benchmarks/mips-before-after.jpg)

|Benchmark|V20 Stock|V20 Turbo|Improvement|
|---|---|---|---|
|General Instructions|0.19|0.29|52.63%|
|Integer Instructions|0.32|0.49|53.12%|
|Memory To Memory|0.26|0.41|57.69%|
|Register To Register|0.39|0.60|53.85%|
|Register To Memory|0.33|0.51|54.55%|
|Overall Performance|0.30|0.46|53.33%|

MIPS also shows that our overclocked NEC V20 is over twice as fast as a stock IBM 5150 running an Intel 8088 CPU.

### Benchmarking Conclusions

As we can see, the speedup on all fronts is in the region of 50-55%, which is a massive improvement for around £6 worth of components. According to [MIPS](#mips), with the addition of the V20 and the overclock this machine is now twice as fast as a standard IBM PC. I haven't encountered any stability issues but my testing is ongoing and of course, if I come across them I will document them here.

Finally, of course benchmarks are entirely artificial and don't necessarily reflect real world results. In my testing I have found that, without exception, every single game on this machine (and I have a fair few) is more playable with massively reduced slowdowns and stuttering. That's a hard thing to quantify, however, so with that in mind I am working on a series of comparison videos which should hopefully be available [on my YouTube channel](https://www.youtube.com/ctrlaltrees) soon.

## PC-SPRINT v2

The above is all well and good, of course, but with the potential for DMA-related problems I decided that it would be worth attempting to improve the design. Although I haven't run into these problems myself and I'm not sure how I'll test it, it will be a fun project and an opportunity to teach myself some things about KiCAD, PCB fabrication and early PCs. With all that in mind, the PC-SPRINT v2 will aim to seamlessly switch back to the stock clock speed whenever there is DMA activity, eliminating the possibility of lockups.

![3D Render of PC-SPRINT v2](PC-SPRINT%20v2/Images/render.png)

** PC-SPRINT v2 now has its own README with regular development updates [here](PC-SPRINT%20v2/README.md). **

## License

The original  design was released under a license analogous to the modern-day GPL, so I have attached that license here. The PC-SPRINT is therefore assumed to comply with the [Open Hardware Specification](https://en.wikipedia.org/wiki/Open-source_hardware).