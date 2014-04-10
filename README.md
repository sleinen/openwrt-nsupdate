# DNS UPDATE (RFC 2136) support for OpenWRT

Many Internet users get a dynamic IPv4 address from their ISP, and use
a "router" (actually a NAT) to give Internet access to devices on the
"internal" network.

But it is often desirable to have a stable handle for whatever public
IPv4 address is currently used.  A DNS hostname is the obvious choice
here.  When the router notices that the ISP assigned it a new IPv4
address, it should be able to update the information (an "A" record)
in DNS.

A popular method for updating DNS information is the HTTP-based DynDNS
protocol.  Many routers support it.

But there is also a "native" update method that's part of the DNS
standard itself.  It is described in RFC 2136, "Dynamic Updates in the
Domain Name System (DNS UPDATE)" by Paul Vixie et al. (1997).

If your DNS provider supports RFC 2136 (DNS UPDATE), they should
provide you with a named key for your zone.  It should be comprised of
two related files, a K<foo>.key file and a K<foo>.private file.  You
need to put these files on the router.

Based on Justin Foell's instructions on
http://www.foell.org/justin/diy-dynamic-dns-with-openwrt-bind/, I have
written a script to dynamically update the router's DNS A record when
the WAN interface is brought up or changes its IPv4 address.

The script includes installation instructions.  Note that it needs to
be parametrized with the correct hostname, authoritative DNS server,
etc.  All the parametrization should be concentrated near the top of
the script.

Compared to Justin's original script, I added some logging to syslog.
