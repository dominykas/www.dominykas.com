---
published: 2010-05-16T23:42:46+00:00
tags: mysql, openvz, proxmox, ubuntu, virtualbox, vm, geeky-stuff
---

# (Solved) troubles with Ubuntu, VirtualBox, OpenVZ/Proxmox and MySQL

<p>Positive start: my new Dell XPS 8100 is now ready for work. To achieve that I had to overcome a couple of puzzlers. They were mostly related to my weird requirements, which I guess are not the common set up path…<br>
<span id="more-108"></span></p>
<h2>The weird setup</h2>
<ul>
<li>The choice of desktop OS is sort of trivial – Ubuntu 10.04 Lucid Lynx. The reasoning is simple – 99% of things just work and I’m quite familiar with it. The active community plays a large part too.</li>
<li><a href="http://www.virtualbox.org/">VirtualBox</a> as the main virtualizer. I’m already a bit familiar with it, and I like its small footprint and the fact that it is easy to setup. I also made a stupid mistake of activating my Windows 7 inside of it, before trying out other VM software. At the end of the day – with guest additions installed, it is absolutely amazing and I have no problems there. Seriously – <a href="http://twitter.com/dymonaz/status/13877378744">I can watch YouTube inside Win7 inside a VM</a> practically without glitches!</li>
<li><a href="http://pve.proxmox.com/wiki/Main_Page">Proxmox Virtual Environment</a> inside the aforementioned Virtualbox. Now, some might say I’m crazy to run a VM inside a VM, but using <a href="http://pve.proxmox.com/wiki/Container_and_Full_Virtualization">containers is far more efficient</a> (especially due to low RAM usage) than running real VMs. Considering OpenVZ was not included in Lucid, and LXC is by far not ready (read: I don’t have enough time to learn everything without proper documentation), Proxmox was an easy choice to make. I’m already using it in production and I’m really happy with how easy it is to setup and maintain.</li>
<li>Ubuntu Lucid again, to host services (Apache, MySQL, couchdb, etc) inside OpenVZ containers. I absolutely love the <a href="http://wiki.openvz.org/Download/template/precreated">minimal OpenVZ templates</a>. The only reason I’m not going for Debian here is the fact that the releases don’t happen frequently enough for my liking. I may reconsider this down the road – but for now – Ubuntu works out for me better.</li>
</ul>
<h2>Problem 1. Proxmox didn’t like being inside VirtualBox</h2>
<p>I downloaded the “bare metal installer” and tried to start it in a VM. All went well until the first reboot, and then it would just hang after detecting the (virtual) hard disks. Took me a couple of hours of scratching my head, until I installed pure Debian inside VirtualBox. Strangely, during installation, the hard drive was appearing as <code>hda</code>, but after finishing, would all of a sudden change to <code>sda</code>, which obviously made things go really sour.</p>
<p><strong>Solution:</strong> change the IDE controller (VM properties -&gt; Storage) from the default PIIX4 to ICH6. I have no clue what all of this means, but the resulting VM now boots fine.</p>
<h2>Problem 2. <code>fsck</code> during every boot due to “last mount time in the future”</h2>
<p>This one is simple – the VM has no access to the hardware clock, which by default is expected to be set to UTC, so your true time gets double-adjusted (once in the host, once in the guest). To fix edit <code>/etc/default/rcS</code> and <a href="http://forums.virtualbox.org/viewtopic.php?f=3&amp;t=27334">make sure <code>UTC=no</code></a>.</p>
<h2>Problem 3. MySQL won’t start inside Lucid inside OpenVZ</h2>
<p>Considering that Lucid doesn’t really support being the host, or the guest of OpenVZ, this comes as no surprise and the bug is marked as “<a href="https://bugs.launchpad.net/ubuntu/+source/mysql-dfsg-5.1/+bug/566736">Won’t fix</a>“. Luckily, there’s a smart guy, <a href="http://blog.bodhizazen.net/linux/ubuntu-10-04-openvz-templates/">who has a workaround</a>. Solution: edit <code>/etc/init/mysql.conf</code> to have it <code>start on runlevel [2345]</code>, instead of the default method, which depends on networking.</p>
<p>I think, I now have all the ingredients to start working on the <em>???</em> part!</p>