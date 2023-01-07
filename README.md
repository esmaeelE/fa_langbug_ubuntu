# fa_langbug_ubuntu

ubuntu bug 

run a live session of ubuntu 

cd /usr/lib/ubiquity/

change files 


run installer in terminal 



Prove this change will fix bug.

1. Boot system with live installer for example `xubuntu-21.04-desktop-amd64.iso`.
2. Fix file : `/usr/lib/ubiquity/localechooser/post-base-installer`
and add `IR) deflang=fa ;;`.
3. Run ubiquity

Run:
$ ubiquity -d gtk_ui --debug

Logs:
	
	tail -f /var/log/syslog
	tail -f /var/log/installer/debug
	
	
See screenshot taken after install with this change to ubiquity installer.


important directory 

	ubiquity
	localechooser
	pluging

When language of installer set fa, locale chooser works fine but 
when language is English, installed locale is fa_az

find how ubiquity generate log 

	get latest code 
	apt install ubuntu-dev
	apt install devscripts

## Work on bug

get source of package

	pull-lp-source ubiquity
	cd ubiquity-22.10.1/

create a new patch 	

	quilt new fa_ir.diff

add files to patch 

	quilt add d-i/patches/localechooser-post-base-installer.patch

make change to actual file 

	vim d-i/patches/localechooser-post-base-installer.patch

update patch system

	quilt refresh


`debian/changelog` must be changed and add version

	ubiquity (22.10.2) kinetic; urgency=medium

	  *  Add default farsi language for IRAN.

	 -- EsmaeelE <esmaeelEE@protonmail.com>  Wed, 04 May 2022 07:07:53 +0430 


	ubiquity (22.10.1) kinetic; urgency=medium

	  *  Update for kinetic.


build package 

	debuild -S -d 
	or
	debuild -S -d --no-sign
	
generate debdiff

	debdiff ubiquity_22.10.1.dsc ubiquity_22.10.2.dsc > ubiquity_22.10.2.debdiff

place debdiff file as patch to bug-report on launchpad

## links

- https://bugs.launchpad.net/ubuntu/+source/ubiquity/+bug/1891270
- https://packaging.ubuntu.com/html/fixing-a-bug.html
- https://packaging.ubuntu.com/html/patches-to-packages.html
- https://ubuntu-packaging-guide.readthedocs.io/en/latest/ubuntu-packaging-guide/fixing-a-bug-example.html
- https://wiki.ubuntu.com/Ubiquity
- https://code.launchpad.net/ubuntu/+source/ubiquity/+merges
- https://launchpad.net/+search?field.text=Dutch+is+the+native+language+for+a+majority+of+the&x=0&y=0
- https://translations.launchpad.net/+languages/nl
- https://git.launchpad.net/ubuntu/+source/ubiquity/commit/?h=applied/ubuntu/lunar-proposed&id=4d1c3567e74c93d0a00e3f282ae1d7e2b6e1a408
- https://git.launchpad.net/ubuntu/+source/ubiquity/
- https://code.launchpad.net/%7E2bdkid/ubuntu/+source/ubiquity/+git/ubiquity/+merge/432828/+index?ss=1
- اps://bugs.launchpad.net/ubuntu/+source/ubiquity/+bug/1907914/comments/0
- tps://bugs.launchpad.net/ubuntu/+source/ubiquity/+bug/1295627
- https://askubuntu.com/questions/1299522/belgian-formats-when-choosing-us-language-regional-language-settings-issue
- https://bugs.launchpad.net/ubuntu/+source/ubiquity/+bug/1907914
- https://git.launchpad.net/ubiquity/tree/d-i/patches/localechooser-post-base-installer.patch#n100

