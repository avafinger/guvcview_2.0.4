Guvcview 2.0.4 with CMOS Camera (H3 - A64 - A83T)
*************************************************

This is my modified version (2.0.4) that works with OPI (Orange Pi) PC / One / 2Plus / 2E
and BananaPi M64 / Pine64+ with CMOS camera.

Known issues or limitations:
 * Encoding is done by software and not hardware. If you want to use Hardware encoder use FFMPEG provided in another repo.
 * Cannot change FPS

Known issues BananaPi M64 / Pine64+:
 * Controls not working yet

Known issues BananaPi M3 (ov8865 - 8M sensor - 3264 x 2448):
 * If guvcview fails for any reason, the memmory buffer fails to be mapped on next time you run guvcview and board needs a reboot (don't worry, board still stable, it is just for the camera)

Howto Build on OPI / Pine64+ / BananaPi - M3 / M64 
 * clone the repo (OPI/A64): git clone https://github.com/avafinger/guvcview_2.0.4.git
 * cd guvcview_2.0.4
 * Install dependencies (see below)
 * Install linux-headers for your kernel if not already installed (usually /usr/src/linux-headers-your_kernel_version)
	 some may find /usr/src/linux-headers-your_kernel_version-sunxi, if that happens you need to edit Makefile.am and add the sufix '-sunxi'.
 * Run (Ubuntu Xenial or Debian Jessie):


Dependencies:
=============
	sudo apt-get install intltool libtool autotools-dev libsdl1.2-dev libgtk-3-dev portaudio19-dev libpng12-dev libavcodec-dev libavutil-dev libudev-dev libusb-1.0-0-dev libpulse-dev libgsl0-dev libv4l-dev libv4l2rds0 libsdl2-dev



Buid Instructions
=================

	./bootstrap.sh
	./configure --prefix=/usr --disable-sdl2
	make
	sudo make install (*)

(*) before installing the guvcview version 2.0.4 remove any previouly installed version
Make sure is removed completely 

 * Check the version:

	guvcview --version 

	Guvcview version 2.0.4 or just run from menu





How to use Guvcview with s5k4ec (Pine64+):
=========================================

 * get latest kernel version 3.10.104 (longsleep) with s5k4ec DTB "ok" or Armbian new build for A64
 * Xenial 16.04 LTS / Debian Jessie
 * (FIXED) always run guvcview by command line:
	
	
	guvcview -d /dev/video0 -x 1280x720 -r sdl -f yu12

	guvcview -d /dev/video0 -x 1920x1080 -r sdl -f yu12

	or run just guvcview or from the menu



How to use Guvcview with ov8865 (BananaPi M3):
==============================================

 * get linux-sunxi version 3.4.39 and compile the new driver
 * Xenial 16.04 LTS
 * (FIXED) always run guvcview by command line FIRST with 1920x1080:


	guvcview -d /dev/video0 -x 1920x1080 -r sdl -f yu12

	or run just guvcview or from the menu

 * if you need some help:


guvcview --help 



	Usage:
	   guvcview [OPTIONS]
	
	OPTIONS:
	-h,--help                             	:Print help
	-v,--version                          	:Print version
	-w,--verbosity=LEVEL                  	:Set Verbosity level (def: 0)
	-q,--cmos_camera=CAMERA               	:Set CMOS camera use (def: 1)
	-d,--device=DEVICE                    	:Set device name (def: /dev/video0)
	-c,--capture=METHOD                   	:Set capture method [read | mmap (def)]
	-b,--disable_libv4l2                  	:disable calls to libv4l2
	-x,--resolution=WIDTHxHEIGHT          	:Request resolution (e.g 640x480)
	-f,--format=FOURCC                    	:Request format (e.g MJPG)
	-r,--render=RENDER_API                	:Select render API (e.g none; sdl)
	-m,--render_window=RENDER_WINDOW_FLAGS	:Set render window flags (e.g none; full; max)
	-a,--audio=AUDIO_API                  	:Select audio API (e.g none; port; pulse)
	-k,--audio_device=AUDIO_DEVICE        	:Select audio device index for selected api (0..N)
	-g,--gui=GUI_API                      	:Select GUI API (e.g none; gtk3)
	-o,--audio_codec=CODEC                	:Audio codec [pcm mp2 mp3 aac ac3 vorb]
	-u,--video_codec=CODEC                	:Video codec [raw mjpg mpeg flv1 wmv1 mpg2 mp43 dx50 h264 vp80 theo]
	-p,--profile=FILENAME                 	:load control profile
	-j,--video=FILENAME                   	:filename for captured video)
	-i,--image=FILENAME                   	:filename for captured image)
	-y,--video_timer=TIME_IN_SEC          	:time (double) in sec. for video capture)
	-t,--photo_timer=TIME_IN_SEC          	:time (double) in sec. between captured photos)
	-n,--photo_total=TOTAL                	:total number of captured photos)
	-z,--control_panel                    	:Start in control panel mode


Basic Configuration
===================
Dependencies:
-------------

Guvcview depends on the following:
	 - intltool,
	 - autotools, 
	 - libsdl2 or libsdl, 
	 - libgtk-3, 
	 - portaudio19, 
	 - libpng, 
	 - libavcodec, 
	 - libavutil, 
	 - libv4l, 
	 - libudev,
	 - libusb-1.0,
	 - libpulse (optional)
	 - libgsl (optional)

On most distributions you can just install the development 
packages:

	intltool, autotools-dev, libsdl2-dev, libgtk-3-dev, 
	portaudio19-dev, libpng12-dev, libavcodec-dev, libavutil-dev,
	libv4l-dev, libudev-dev, libusb-1.0-0-dev, libpulse-dev, libgsl-dev

GUVCVIEW Author: Paulo Assis (https://sourceforge.net/p/guvcview/)

Build configuration:
--------------------
(./bootstrap.sh; ./configure)

The configure script is generated from configure.ac by autoconf,
the helper script ./bootstrap.sh can be used for this, it will also
run the generated configure with the command line options passed.
After configuration a simple 'make && make install' will build and
install guvcview and all the associated data files.

Data Files:
------------
(language files; image files; gnome menu entry)

guvcview data files are stored by default to /usr/local/share
setting a different prefix (--prefix=BASEDIR) during configuration
will change the installation path to BASEDIR/share.

Built files, src/guvcview and data/gnome.desktop, are dependent 
on this path, so if a new prefix is set a make clean is required 
before issuing the make command. 

After running the configure script the normal, make && make install 
should build and install all the necessary files.    
    
 
guvcview bin:
-------------
(guvcview)

The binarie file installs to the standart location,
/usr/local/bin, to change the install path, configure
must be executed with --prefix=DIR set, this will cause
the bin file to be installed in DIR/bin, make sure 
DIR/bin is set in your PATH variable, or the gnome 
menu entry will fail.

guvcview libraries:
-------------------
(libgviewv4l2core, libgviewrender, libgviewaudio, libgviewencoder)

The core functionality of guvcview is now split into 4 libraries
these will install to ${prefix}/lib and development headers to
${prefix}/include/guvcview-2/libname. 
pkg-config should be use to determine the compile flags.


guvcview.desktop:
-----------------

(data/guvcview.desktop)

The desktop file (gnome menu entry) is built from the
data/guvcview.desktop.in definition and is dependent on the 
configure --prefix setting, any changes to this, must 
be done in data/guvcview.desktop.in.

configuration files:
--------------------
(~/.config/guvcview2/video0)

The configuration file is saved into the $HOME dir when 
exiting guvcview. If a video device with index > 0,
e.g: /dev/video1 is used then the file stored will be
named ~/.config/guvcview2/video1

Executing guvcview
================== 

For instructions on the command line args 
execute "guvcview --help".
