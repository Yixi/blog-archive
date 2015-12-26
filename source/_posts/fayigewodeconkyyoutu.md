title: '发一个我的conky,附效果图。'
tags:
  - conky
  - Linux
  - 原创作品
id: 345
categories:
  - 窗外的世界
date: 2009-09-15 19:45:28
---

![mydesktop](http://blog.liuyixi.com/wp-content/uploads/2009/09/desktop.jpg "mydesktop")

先上一个整个桌面的效果图吧。

那天接触到一个很不错的的系统监视软件，参考着配置帮助，借鉴了网上的一些列子，自己折腾了一天弄出了这样的配置文件。

因为我喜欢显示的信息多一些，所以使用的字体比较小，这样能显示更多的信息，之前在网上看到的那个电脑模型的全屏conky，很牛X，很眩，还有一个直接把桌面改装成了命令行的桌面，很深邃的感觉，之后有空会去尝试一下那样的效果。

好了，废话不多说，放上我的conky配置：
<pre lang="conky" line="1" file="download.txt" colla="+">
background no
font Clean:size=10
#xftfont Sans:size=10
use_xft yes
xftalpha 1.0
update_interval 1.0
total_run_times 0
own_window yes
own_window_type override
own_window_transparent yes
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager
double_buffer yes
minimum_size 300 800
maximum_width 300
draw_shades no
draw_outline no
draw_borders no
draw_graph_borders yes
default_color white
color3 6495ED
default_shade_color black
default_outline_color green
alignment top_right
gap_x 5
gap_y 30
no_buffers yes
uppercase no
cpu_avg_samples 2
override_utf8_locale no
uppercase no # set to yes if you want all text to be in uppercase

TEXT
${color3}System Information ${color}${hr 1}
$color${execi 20 /etc/conky/conky_user.sh}@$nodename - $sysname $kernel on $machine
Uptime: ${alignr}$uptime
RAM:    ${alignr}$mem / $memmax
$memperc%  ${membar 4}
SWAP:   ${alignr}$swap / $swapmax
$swapperc%  ${swapbar 4}
CPU:    ${alignr}$freq_g Ghz
$cpu%  ${cpubar 4}
${cpugraph 20, 300 000000 6495ED}
${color3}Processes ${color}${hr 1}
Name ${alignr}  PID      CPU%    MEM%
${top name 1} ${alignr}${top pid 1}    ${top cpu 1}      ${top mem 1}
${top name 2} ${alignr}${top pid 2}    ${top cpu 2}      ${top mem 2}
${top name 3} ${alignr}${top pid 3}    ${top cpu 3}      ${top mem 3}
${top name 4} ${alignr}${top pid 4}    ${top cpu 4}      ${top mem 4}
${top name 5} ${alignr}${top pid 5}    ${top cpu 5}      ${top mem 5}
${color3}Time &amp; Date ${color}${hr 1}
Time: ${alignr}${time %H:%M}
Date: ${alignr}${time %d/%m/%Y [%V. week]}
${color3}File systems ${color}${hr 1}
${diskiograph 20,300 000000 6495ED}
Root:  ${fs_size /}/${fs_free /} ${fs_bar 6 /}
Soft:  ${fs_size /media/soft}/${fs_free /media/soft} ${fs_bar 6 /media/soft}
Media: ${fs_size /media/media/}/${fs_free /media/media} ${fs_bar 6 /media/media/}
File:  ${fs_size /media/disk/}/${fs_free /media/disk} ${fs_bar 6 /media/disk/}
Study: ${fs_size /media/study/}/${fs_free /media/study} ${fs_bar 6 /media/study/}
${color3}Network ${color}${hr 1}
Ip address: ${alignr}${addr eth0}
Rate:    ${alignr}${execi 20 /etc/conky/conky_wifi.sh} Mb/s
Down ${downspeed eth0} k/s ${alignr}Up ${upspeed eth1} k/s
${downspeedgraph eth0 20,115 000000 6495ED} ${alignr}${upspeedgraph eth0 20,115 000000 6495ED}
Total ${totaldown eth0} ${alignr}Total ${totalup eth0}
${color3}Mails ${color}${hr 1}
Gmail: ${alignr}${execi 60 /etc/conky/gmail.sh}
${color3}Battery ${color}${hr 1}
$battery_percent %  $battery_bar
${color3}Ports ${color}${hr 1}
Inbound: ${tcp_portmon 1 32767 count}  Outbound: ${tcp_portmon 32768 61000 count}${alignr}ALL: ${tcp_portmon 1 65535 count}
Inbound Connection ${alignr} Local Service/Port
${tcp_portmon 1 32767 rhost 0} ${alignr} ${tcp_portmon 1 32767 lservice 0}
${tcp_portmon 1 32767 rhost 1} ${alignr} ${tcp_portmon 1 32767 lservice 1}
${tcp_portmon 1 32767 rhost 2} ${alignr} ${tcp_portmon 1 32767 lservice 2}
${tcp_portmon 1 32767 rhost 3} ${alignr} ${tcp_portmon 1 32767 lservice 3}
${tcp_portmon 1 32767 rhost 4} ${alignr} ${tcp_portmon 1 32767 lservice 4}
Outbound Connection ${alignr} Remote Service/Port
${tcp_portmon 32768 61000 rhost 0} ${alignr} ${tcp_portmon 32768 61000 rservice 0}
${tcp_portmon 32768 61000 rhost 1} ${alignr} ${tcp_portmon 32768 61000 rservice 1}
${tcp_portmon 32768 61000 rhost 2} ${alignr} ${tcp_portmon 32768 61000 rservice 2}
${tcp_portmon 32768 61000 rhost 3} ${alignr} ${tcp_portmon 32768 61000 rservice 3}
${tcp_portmon 32768 61000 rhost 4} ${alignr} ${tcp_portmon 32768 61000 rservice 4}</pre>
![bar](http://blog.liuyixi.com/wp-content/uploads/2009/09/bar.jpg "bar")