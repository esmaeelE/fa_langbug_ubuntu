quilt new farsi_iran.diff
quilt add d-i/patches/localechooser-post-base-installer.patch 
quilt edit d-i/patches/localechooser-post-base-installer.patch 
quilt diff 
quilt refresh 
quilt diff 
quilt header --dep3 -e 
vim debian/changelog
debuild -S -d 
cd ..
ls
debdiff ubiquity_22.10.2.dsc ubiquity_22.10.3.dsc > debdiff.txt
vim debdiff.txt 
ls
cd ubiquity-22.10.2/
history 
quilt applied 
quilt diff 

d-i/source/localechooser/post-base-installer.d/05localechooser
d-i/patches/localechooser-post-base-installer.patch

