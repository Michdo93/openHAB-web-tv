# openHAB-web-tv
Using exec binding and ssh to use a remote computer to watch TV streams via VLC or a browser.

## Items

You have to create for each live stream a `Switch` item. Later a rule will trigger when a `Switch` item changed to `ON`. If it is `Kabel1`, `Sat1`, `Pro7` or `sixx` a web browser will be opened if it is not previously mentioned VLC will be opened.

```
Group Webtv "Webtv" <screen>

Switch Webtv_Ard "ARD" (Webtv)
Switch Webtv_Ard_Alpha "ARD Alpha" (Webtv)
Switch Webtv_Ard_Tagesschau "ARD Tagesschau" (Webtv)
Switch Webtv_3Sat "3Sat" (Webtv)
Switch Webtv_Deutsche_Welle "Deutsche Welle" (Webtv)
Switch Webtv_Ard_Sportschau_2 "ARD Sportschau 2" (Webtv)
Switch Webtv_ZDF "ZDF" (Webtv)
Switch Webtv_ZDF_info "ZDF info" (Webtv)
Switch Webtv_ZDF_neo"ZDF neo" (Webtv)
Switch Webtv_HR "HR" (Webtv)
Switch Webtv_RBB_Berlin "RBB Berlin" (Webtv)
Switch Webtv_RBB_Brandenburg "RBB Brandenburg" (Webtv)
Switch Webtv_WDR "WDR" (Webtv)
Switch Webtv_NASA_TV_Public "NASA TV Pulic HD" (Webtv)
Switch Webtv_NASA_TV_Media "NASA TV Media HD" (Webtv)
Switch Webtv_MDR_SachsenAnhalt "MDR Sachsen-Anhalt" (Webtv)
Switch Webtv_MDR_Sachsen "MDR Sachsen" (Webtv)
Switch Webtv_MDR_Thueringen "MDR Thüringen" (Webtv)
Switch Webtv_Phoenix "Phoenix" (Webtv)
Switch Webtv_BR_Nord "BR Nord" (Webtv)
Switch Webtv_BR_Sued "BR Süd" (Webtv)
Switch Webtv_SWR_BW "SWR BW" (Webtv)
Switch Webtv_SWR_RP "SWR RP" (Webtv)
Switch Webtv_NDR_SchleswigHolstein "NDR Schleswig-Holstein" (Webtv)
Switch Webtv_NDR_MecklenburgVorpommern "NDR Mecklenburg-Vorpommern" (Webtv)
Switch Webtv_NDR_Niedersachsen "NDR Niedersachsen" (Webtv)
Switch Webtv_NDR_Hamburg "NDR Hamburg" (Webtv)
Switch Webtv_Arte_DE "Arte DE" (Webtv)
Switch Webtv_Arte_FR "Arte FR" (Webtv)
Switch Webtv_kika "kika" (Webtv)
Switch Webtv_Kabel1 "Kabel 1" (Webtv)
Switch Webtv_Sat1 "Sat1" (Webtv)
Switch Webtv_Pro7 "Pro7" (Webtv)
Switch Webtv_sixx "sixx" (Webtv)
```

## Rules

Besides the `Switch` items for each live stream changed to `ON` there must be rules if they are changed to `OFF` for closing VLC or the browser.

```
rule "Webtv changed to ON"
when
    Item Webtv_Ard changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://mcdn.daserste.de/daserste/de/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_Ard_Alpha changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://mcdn.br.de/br/fs/ard_alpha/hls/de/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_Ard_Tagesschau changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://tagesschau.akamaized.net/hls/live/2020115/tagesschau/tagesschau_1/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_3Sat changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://zdf-hls-18.akamaized.net/hls/live/2016501/dach/high/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_Deutsche_Welle changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://dwamdstream111.akamaized.net/hls/live/2017972/dwstream111/stream05/streamPlaylist.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_Ard_Sportschau_2 changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://ardevent2.akamaized.net/hls/live/681512/ardevent2_geo/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_ZDF changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","http://zdf-hls-15.akamaized.net/hls/live/2016498/de/veryhigh/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_ZDF_info changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://zdf-hls-17.akamaized.net/hls/live/2016500/de/high/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_ZDF_neo changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://zdf-hls-16.akamaized.net/hls/live/2016499/de/high/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_HR changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://hrhls.akamaized.net/hls/live/2024525/hrhls/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_RBB_Berlin changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://rbb-hls-berlin.akamaized.net/hls/live/2017824/rbb_berlin/index.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_RBB_Brandenburg changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://rbb-hls-brandenburg.akamaized.net/hls/live/2017825/rbb_brandenburg/index.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_WDR changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://mcdn.wdr.de/wdr/wdrfs/de/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_NASA_TV_Public changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://ntv1.akamaized.net/hls/live/2014075/NASA-NTV1-HLS/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_NASA_TV_Media changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://ntv2.akamaized.net/hls/live/2013923/NASA-NTV2-HLS/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_MDR_SachsenAnhalt changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://mdrtvsahls.akamaized.net/hls/live/2016879/mdrtvsa/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_MDR_Sachsen changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://mdrtvsnhls.akamaized.net/hls/live/2016928/mdrtvsn/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_MDR_Thueringen changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://mdrtvthhls.akamaized.net/hls/live/2016880/mdrtvth/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_Phoenix changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","http://zdf-hls-19.akamaized.net/hls/live/2016502/de/high/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_BR_Nord changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://mcdn.br.de/br/fs/bfs_nord/hls/de/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_BR_Sued changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://mcdn.br.de/br/fs/bfs_sued/hls/de/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_SWR_BW changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://swrbwd-hls.akamaized.net/hls/live/2018672/swrbwd/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_SWR_RP changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://swrrpd-hls.akamaized.net/hls/live/2018676/swrrpd/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_NDR_SchleswigHolstein changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://mcdn.ndr.de/ndr/hls/ndr_fs/ndr_sh/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_NDR_MecklenburgVorpommern changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://mcdn.ndr.de/ndr/hls/ndr_fs/ndr_mv/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_NDR_Niedersachsen changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://mcdn.ndr.de/ndr/hls/ndr_fs/ndr_nds/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_NDR_Hamburg changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://mcdn.ndr.de/ndr/hls/ndr_fs/ndr_hh/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_Arte_DE changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://artesimulcast.akamaized.net/hls/live/2030993/artelive_de/index.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_Arte_FR changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://artesimulcast.akamaized.net/hls/live/2031003/artelive_fr/index.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_kika changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/vlc","--video-on-top","--fullscreen","https://kikageohls.akamaized.net/hls/live/2022693/livetvkika_de/master.m3u8")
end

rule "Webtv changed to ON"
when
    Item Webtv_Kabel1 changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/python3","selenium_kabel1.py")
end

rule "Webtv changed to ON"
when
    Item Webtv_Sat1 changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/python3","selenium_sat1.py")
end

rule "Webtv changed to ON"
when
    Item Webtv_Pro7 changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/python3","selenium_pro7.py")
end

rule "Webtv changed to ON"
when
    Item Webtv_sixx changed to ON
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/python3","selenium_sixx.py")
end

rule "Webtv changed to OFF"
when
    Item Webtv_Ard changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_Ard_Alpha changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_Ard_Tagesschau changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_3Sat changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_Deutsche_Welle changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_Ard_Sportschau_2 changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_ZDF changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_ZDF_info changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_ZDF_neo changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_HR changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_RBB_Berlin changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_RBB_Brandenburg changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_WDR changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_NASA_TV_Public changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_NASA_TV_Media changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_MDR_SachsenAnhalt changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_MDR_Sachsen changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_MDR_Thueringen changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_Phoenix changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_BR_Nord changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_BR_Sued changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_SWR_BW changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_SWR_RP changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_NDR_SchleswigHolstein changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_NDR_MecklenburgVorpommern changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_NDR_Niedersachsen changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_NDR_Hamburg changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_Arte_DE changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_Arte_FR changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_kika changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/killall","/usr/bin/vlc")
end

rule "Webtv changed to OFF"
when
    Item Webtv_Kabel1 changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/pkill","-f ","firefox")
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/pkill","-9","-f","selenium_kabel1.py")
end

rule "Webtv changed to OFF"
when
    Item Webtv_Sat1 changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/pkill","-f ","firefox")
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/pkill","-9","-f","selenium_sat1.py")
end

rule "Webtv changed to OFF"
when
    Item Webtv_Pro7 changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/pkill","-f ","firefox")
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/pkill","-9","-f","selenium_pro7.py")
end

rule "Webtv changed to OFF"
when
    Item Webtv_sixx changed to OFF
then
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/pkill","-f ","firefox")
    executeCommandLine("/usr/bin/sshpass","-p","<password>","/usr/bin/ssh","-t","-o","StrictHostKeyChecking=no","<user>@<ip>","/usr/bin/sudo","/usr/bin/pkill","-9","-f","selenium_sixx.py")
end
```

That the rules work, please add following to `/etc/openhab/misc/exec.whitelist`:

```
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://mcdn.daserste.de/daserste/de/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://mcdn.br.de/br/fs/ard_alpha/hls/de/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://tagesschau.akamaized.net/hls/live/2020115/tagesschau/tagesschau_1/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://zdf-hls-18.akamaized.net/hls/live/2016501/dach/high/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://dwamdstream111.akamaized.net/hls/live/2017972/dwstream111/stream05/streamPlaylist.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://ardevent2.akamaized.net/hls/live/681512/ardevent2_geo/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen http://zdf-hls-15.akamaized.net/hls/live/2016498/de/veryhigh/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://zdf-hls-17.akamaized.net/hls/live/2016500/de/high/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://zdf-hls-16.akamaized.net/hls/live/2016499/de/high/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://hrhls.akamaized.net/hls/live/2024525/hrhls/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://rbb-hls-berlin.akamaized.net/hls/live/2017824/rbb_berlin/index.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://rbb-hls-brandenburg.akamaized.net/hls/live/2017825/rbb_brandenburg/index.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://mcdn.wdr.de/wdr/wdrfs/de/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://ntv1.akamaized.net/hls/live/2014075/NASA-NTV1-HLS/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://ntv2.akamaized.net/hls/live/2013923/NASA-NTV2-HLS/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://mdrtvsahls.akamaized.net/hls/live/2016879/mdrtvsa/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://mdrtvsnhls.akamaized.net/hls/live/2016928/mdrtvsn/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://mdrtvthhls.akamaized.net/hls/live/2016880/mdrtvth/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen http://zdf-hls-19.akamaized.net/hls/live/2016502/de/high/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://mcdn.br.de/br/fs/bfs_nord/hls/de/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://mcdn.br.de/br/fs/bfs_sued/hls/de/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://swrbwd-hls.akamaized.net/hls/live/2018672/swrbwd/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://swrrpd-hls.akamaized.net/hls/live/2018676/swrrpd/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://mcdn.ndr.de/ndr/hls/ndr_fs/ndr_sh/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://mcdn.ndr.de/ndr/hls/ndr_fs/ndr_mv/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://mcdn.ndr.de/ndr/hls/ndr_fs/ndr_nds/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://mcdn.ndr.de/ndr/hls/ndr_fs/ndr_hh/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://wdrfs247.akamaized.net/hls/live/681509/wdr_msl4_fs247/index.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://artesimulcast.akamaized.net/hls/live/2030993/artelive_de/index.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://artesimulcast.akamaized.net/hls/live/2031003/artelive_fr/index.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/vlc --video-on-top --fullscreen https://kikageohls.akamaized.net/hls/live/2022693/livetvkika_de/master.m3u8"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/python3 selenium_kabel1.py"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/python3 selenium_sat1.py"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/python3 selenium_pro7.py"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/python3 selenium_sixx.py"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/sudo /usr/bin/pkill -f firefox"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/sudo /usr/bin/pkill -9 -f selenium_kabel1.py"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/sudo /usr/bin/pkill -9 -f selenium_sat1.py"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/sudo /usr/bin/pkill -9 -f selenium_pro7.py"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/sudo /usr/bin/pkill -9 -f selenium_sixx.py"
/usr/bin/sshpass -p <password> /usr/bin/ssh -t -o StrictHostKeyChecking=no <user>@<ip> "/usr/bin/sudo /usr/bin/killall /usr/bin/vlc"
```

You have to replace `<user>` and `<password>` with the username and password of your remote computer. Also you have to change `<ip>` with the ip address of your remote computer.

## Sitemaps

At least you have to add following to your sitemap:

```
Text label="Webtv" icon=screen {
    Switch item=Webtv_Ard label="ARD"
    Switch item=Webtv_Ard_Alpha label="ARD Alpha"
    Switch item=Webtv_Ard_Tagesschau label="ARD Tagesschau"
    Switch item=Webtv_3Sat label="3Sat"
    Switch item=Webtv_Deutsche_Welle label="Deutsche Welle"
    Switch item=Webtv_Ard_Sportschau_2 label="ARD Sportschau 2"
    Switch item=Webtv_ZDF label="ZDF"
    Switch item=Webtv_ZDF_info label="ZDF info"
    Switch item=Webtv_ZDF_neo label="ZDF neo"
    Switch item=Webtv_HR label="HR"
    Switch item=Webtv_RBB_Berlin label="RBB Berlin"
    Switch item=Webtv_RBB_Brandenburg label="RBB Brandenburg"
    Switch item=Webtv_WDR label="WDR"
    Switch item=Webtv_NASA_TV_Public label="NASA TV Pulic HD"
    Switch item=Webtv_NASA_TV_Media label="NASA TV Media HD"
    Switch item=Webtv_MDR_SachsenAnhalt label="MDR Sachsen-Anhalt"
    Switch item=Webtv_MDR_Sachsen label="MDR Sachsen"
    Switch item=Webtv_MDR_Thueringen label="MDR Thüringen"
    Switch item=Webtv_Phoenix label="Phoenix"
    Switch item=Webtv_BR_Nord label="BR Nord"
    Switch item=Webtv_BR_Sued label="BR Süd"
    Switch item=Webtv_SWR_BW label="SWR BW"
    Switch item=Webtv_SWR_RP label="SWR RP"
    Switch item=Webtv_NDR_SchleswigHolstein label="NDR Schleswig-Holstein"
    Switch item=Webtv_NDR_MecklenburgVorpommern label="NDR Mecklenburg-Vorpommern"
    Switch item=Webtv_NDR_Niedersachsen label="NDR Niedersachsen"
    Switch item=Webtv_NDR_Hamburg label="NDR Hamburg"
    Switch item=Webtv_Arte_DE label="Arte DE"
    Switch item=Webtv_Arte_FR label="Arte FR"
    Switch item=Webtv_kika label="kika"
    Switch item=Webtv_Kabel1
    Switch item=Webtv_Sat1
    Switch item=Webtv_Pro7
    Switch item=Webtv_sixx
}
```
