# Install Linux Mint on Asus A15

## Problems & Root Causes

1. The 5.4 Kernel included with Linux Mint 20.1 predates the release of the laptop, and more importantly, the AMD Ryzen 7 4800U.
2. The open source driver doesn't work well with the nvidia 1660ti
3. This laptop uses an AMD Ryzen 4800U with an Nvidia 1660ti video card by internally routing the output of the nvidia card through the integrated AMD Vega graphics card. Even in Windows, the compatability for this is't great (for example, some VR headsets don't work properly as they use the AMD card rather than nvidia).
4. Disabling certain features also disables the touchpad, which has the latent effect of the touchpad not working in "compatability mode". This extends to every mode when the fix is to mimic this behavior.

> Advising the "fix" being to plug in a mouse is absolutely rediculous. May as well tell them to throw their laptop in the trash and buy a desktop

## Install Procedure

1. Download [Linux Mint 20.1](https://www.linuxmint.com/edition.php?id=284) and write to usb using [rufus](https://rufus.ie/en_US/).
2. [Boot to usb](https://www.asus.com/me-en/support/FAQ/1013017) and with the first option selected in grub, hit the letter `e` to edit the config prior to booting
3. Modify the linux kernel line replacing `quiet splash` with `nomodeset`, hit `ctrl+x` or `f10` to boot into the installer
  > Note that the laptop basically functions as intended + touchpad works. If you select compatability mode in the advanced options the touchpad will not function during the installation.
4. Install Linux Mint as usual
5. Boot Mint from the hard repeating step 3
6. Edit `/etc/default/grub` changing `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"` to `GRUB_CMDLINE_LINUX_DEFAULT="nomodeset"` then run `update-grub2` so that you don't go insane doing step 3 every time you need to boot until it's fixed.
7. Boot into Mint and config/install updates/etc as you would with any new OS install **do not install the propertary nvidia drivers**
8. Reboot and install [Ubuntu Mainline Kernel Installer](https://github.com/bkw777/mainline) note that you only have to follow these steps:
```
sudo add-apt-repository ppa:cappelikan/ppa
sudo apt update
sudo apt install mainline
```
8. Use mainline kernel installer to install a kernel >= 4.6 - and if you're not about that "do a million changes and expect them to all perfectly first try yolo" life like me, reboot into the new kernel to confirm it's working properly. Note that screen brightness and perhaps other keyboard shortcuts may now begin to function that weren't working before.
9. Open driver manager and install the recommended proprietary nvidia-driver version. It will say "NVIDIA driver metapackage" under it if it is the proprietary one (the open source one - which does not work well - will say "Nouveau display driver")
10. Revert #6 by editing `/etc/default/grub` and changing `GRUB_CMDLINE_LINUX_DEFAULT="nomodeset"` to `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"` then running `update-grub2` to apply the changes.
11. Boot into your minty fresh OS running only the finest responsibly sourced kernel and drivers

## Works

1. Touchpad
2. Both graphics cards
3. Keyboard + function-keys
4. Audio & audio routing (this is broken out of the box in Ubuntu proper)

## Don't work

1. Display port over USB-C (I hope I can fix with trying different kernels - note that newest kernels may depend on packages that are too new for other packages on your system)
2. ??? (I'm sure there's tons of broken crap, I just haven't found it yet)


## Rant / Story Time

Unfortunately, there are countless bad guides for installing Linux Mint on the Asus A15, Asus A17, and other similar notebooks on the internet. [ex 1](https://gist.github.com/danialmalik/648311826baaa4883b0936686a0d79d1) [ex 2](https://www.reddit.com/r/linuxhardware/comments/hbqa7r/issues_ryzen_4000_4800u_compatibility_ubuntu_2004/), and while not specific to this issue [this post](https://forums.linuxmint.com/viewtopic.php?t=350317) gets an honorable mention because the post ends with what is essentially an allusion to the problem being due to the 77.6% usage of OP's hard drive.

Although I'm more experienced and should know better, I still get caught up in the trap of taking advice from random google searches when my own knowledge exceeds what those searches will unearth. For this reason, making this guide both for the benefit of others and my own benefit when down the road I surely forget all about this experience and move on.

I hate how prescriptive advice has become on the Internet these days. It's as if people want to just cheat on their homework. No one seems to care WHY the answer is the answer these days, they just want that juicy succulent answer so they can move on. In this case, it is absolutely critical to understand _WHY_ this is happening, because this has lead to the trove of misguided answers that lead to less-broken-yet-more-broken installs that don't paint linux in the best of lights for anyone who's experience with linux is limited to this.

Linux desktop distributions have tradeoffs to make. They must balance openness, features, speed, performance, battery life, hardware support, the list goes on. Linux Mint is a fantastic distribution, however, you should know that the maintainers tend to err on the side of more stability at the cost of not being completely current.

[Linux Mint Ulyssa](https://www.linuxmint.com/rel_ulyssa.php) is the latest version of Mint, but at the time of writing the latest kernel is 5.4 which was released [2019-11-24](https://www.kernel.org/category/releases.html). This laptop was the first laptop released with the AMD Ryzen 7 4800U, and was released on [2nd June 2020](https://gadgets.ndtv.com/asus-tuf-a15-price-in-india-94088). Do you see the problem here?

Alright, I'm done ranting
