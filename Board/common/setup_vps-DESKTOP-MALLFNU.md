# setup_vps

Today I use vultr VPS and set up a SSR server.
A very good guide[https://www.tipsforchina.com/how-to-setup-a-fast-shadowsocks-server-on-vultr-vps-the-easy-way.html]

1. Go to the vultr to render a cloud instance.
2. Choose the location and system.
* Tokyo, Japan	 hnd-jp-ping.vultr.com
 * Singapore	 sgp-ping.vultr.com
 * Silicon Valley, California	 sjo-ca-us-ping.vultr.com
*  Los Angeles, California	 lax-ca-us-ping.vultr.com
 * Seattle, Washington	 wa-us-ping.vultr.com
*  Frankfurt, DE	 fra-de-ping.vultr.com
*  Amsterdam, NL	 ams-nl-ping.vultr.com
*  Paris, France	 par-fr-ping.vultr.com
*  London, UK	 lon-gb-ping.vultr.com
 * New York (NJ)	 nj-us-ping.vultr.com
 * Chicago, Illinois	 il-us-ping.vultr.com
*  Atlanta, Georgia	 ga-us-ping.vultr.com
*  Miami, Florida	 fl-us-ping.vultr.com
*  Dallas, Texas	 tx-us-ping.vultr.com
*  Sydney, Australia	 syd-au-ping.vultr.com

3. Login by Putty
4. Run the following command:
>>  wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh
>
>> chmod +x shadowsocksR.sh
>
>> ./shadowsocksR.sh 2>&1 | tee shadowsocksR.log

type the pass word, port, 12  (which is chacha20) and 1 (which is origin) and 3 which is "http_simple_compatible".

By the way: the way to change the setting is
nano /etc/shadowsocks.json
/etc/init.d/shadowsocks restart



Download the windows client:
https://github.com/shadowsocksrr/shadowsocksr-csharp/releases

