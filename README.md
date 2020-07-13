# Network Loom

The internet is a messy, complex weave of devices, people, and connections. It's also very noisy out there with all the background network scans and probes our systems are subjected to every day. That constant background noise makes life harder for IT pros whose job it is to manage and monitor firewalls, routers, and intrusion detection systems (IDS). I want to help keep the noise down and maybe even stop malicious connections from happening in the process.

This project has sensors deployed across the internet waiting for scanners and hackers to hit them. Those scanners gather intelligence about traffic sources and I publishes the results. You can use that information for monitoring connections to your own networks or blackholing traffic. It's my hope that people looking for easy targets will connect to my sensors first, get documented, and then later be denied by you.

## Network Intelligence

Sensors are distributed across major cloud providers like Azure, AWS, DigitalOcean, and others. Some of my sensors also have a physical presence in colocation facilities. Activity is recorded when attackers attempt logons using well-known credentials over services like SSH or MySQL. The same happens when sensitive services like SSH, VNC, and RDP are port scanned. The source of that connection is added to our lists and made available to you.

## Lists

I'm currently making three lists available - [*port_scanners.txt*](bad_logons.txt), [*bad_logons.txt*](port_scanners.txt), and [complete.txt](complete.txt). The first two files have self-explanatory names, and the third file is a combination of all traffic sources. Having the lists in simple text makes them easy to parse and use in scripts. Feel free to use one or both to filter traffic on your networks. Sometime in the future I'll publish Snort rulesets based on these lists as well.

## License

This project is licensed under the **Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International** license - see [https://creativecommons.org/licenses/by-nc-nd/4.0/legalcode]. For commercial licensing or research inquiries please contact tylerhart84@gmail.com.

## FAQ

1. **Who are you trying to catch?** I'm trying to identify both benign organizations and malicious threat actors who are probing systems and possibly attempting access across the internet.

1. **Is all port scanning bad?** Absolutely not! There are many benign organizations who use port scanning as part of their research and for monitoring internet "health". Many for-profit and non-profit organizations routinely scan the entire IP address space and collect metrics. With that being said, there are also many individuals and governmental organization who scan our systems looking for "soft targets" they can infiltrate. It can often be difficult to tell one from the other, and there is no centralized mechanism to "opt out" of being scanned.

1. **What services are you monitoring?** Sensors are operating on ports commonly targetted by attackers including SSH, MySQL, ElasticSearch, VNC, etc. Listeners periodically change IP addresses and port behavior to avoid discovery by threat actors.

1. **How do you avoid false positives?** Part of the false positive prevention we've implemented is NOT listening for HTTP or HTTPS traffic. Search engines and other crawlers would create a huge hassle if we listened for web traffic. To trip a sensor and generate an alert you'd have to be connecting specifically to a sensitive, non-web service. ICMP traffic won't trigger an alert either, so just sending an echo request ("ping") to a sensor won't land you on a list. Basically, you need to go out of your way to be searching for vulnerable hosts to trigger an alert.

1. **How long does an address stay on your lists?** I'm automatically "aging-out" addresses between 30 and 60 days. There is some randomness in the process to avoid discovery of a sensor by threat actors. Repeated alerts from the same address reset the clock and delay age-out.

1. **My IP address is on a list - will you remove it?** No, I won't remove IP addresses manually. A device operating on your network was either attempting to probe a sensitive service on my sensors or logon using password guessing. It's one thing to ping an IP address or attempt to crawl a website; It's quite another to probe services or attempt logon to a system you don't own.

1. **Can I use a list on my personal systems?** Absolutely! Protecting our networks at home is important.

1. **Can I use a list on my employer's systems?** I'm charging commercial users a small licensing fee to help keep the lights on here. Please contact me at tylerhart84@gmail.com for more information.

1. **Can I resell or redistribute your lists?** Not without permission - please contact me if you're interested in reselling or redistributing my lists.
