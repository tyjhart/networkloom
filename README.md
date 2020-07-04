# Network Loom

The internet is a complex weave of devices, people, and connections. Devices are the warp, people are the weft, and the connections between them bring it all together. Unfortunately, not all people are good and not all connections are made for the right reasons. I want to help stop those bad connections from happening and give people tools to defend themselves against cyber criminals and other bad actors. This project gathers intelligence about threat actors and publishes the results that you can use for monitoring or blackholing traffic. Multiple lists are compiled for monitoring or filtering your network traffic. It's my hope that people looking for easy targets will connect to me first, be documented, and their connections then denied by you.

## Network Intelligence

I'm gathering intelligence about threat actors and the connections they make through distributed listeners and other methods. Listener servers are distributed across major cloud providers like Azure, AWS, DigitalOcean, and others. Activity is recorded when attackers attempt logons using well-known credentials over certain services like SSH or MySQL. The source of that connection is added to our lists and made available to you. The same happens when sensitive services like VNC and RDP are port scanned.

## Lists

I'm currently making two lists available - *port_scanners.txt* and *bad_logons.txt*. Feel free to use one or both to filter traffic on your networks. Sometime in the future I'll publish a Snort ruleset as well.

## FAQ

1. **What services are you monitoring?** Listeners are operating on ports commonly targetted by attackers including SSH, MySQL, ElasticSearch, VNC, etc. Listeners periodically cycle through random ports to avoid discovery by threat actors.

1. **How do you avoid false positives?** Part of the false positive prevention we've implemented is NOT listening for HTTP or HTTPS traffic. Web crawlers would create a huge hassle if we did listen for web traffic. To trip a listener and generate an alert you'd have to be connecting specifically to a sensitive, non-web service. ICMP traffic won't trigger an alert either. Basically, you need to go out of your way to be searching for vulnerable hosts to trigger an alert on a listener.

1. **How long does an address stay on your lists?** I'm automatically "aging-out" addresses between 30 and 60 days. There is some randomness in the process to avoid discovery of a listener by threat actors. Repeated alerts from the same address reset the clock.

1. **My IP address is on a list - will you remove it?** No, I won't remove IP addresses manually from the list. A device operating on your network was either attempting to probe a sensitive service on listener servers or logon using password guessing. It's one thing to ping an IP address or attempt to crawl a website; It's quite another to probe services or attempt logon to a server you don't own.

1. **Can I use a list on my personal network?** Absolutely! Protect our networks at home is important.

1. **Can I use a list on my employer's network?** Sure! One of my goals is to give back to the IT security profession and help other professionals secure their networks at work.

1. **Can I resell or redistribute your lists?** No - please contact me if you're interested in reselling or redistributing my lists.
