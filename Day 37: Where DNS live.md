## Where DNS Lives
DNS Servers (Globally Distributed). It's a distributed system.

## Four types of DNS Servers
1. Recursive Resolver (Your first stop)
2. Root Name servers
3. TLD Name servers
4. Authoritative Name server

My computer talks to the recursive resolver server first. It is provided by the ISP or the Public DNS service.
This server looks for the IP that matches my domain address. Next, Root name servers—There are 13 root servers worldwide.
managed by ICANN. They don’t know the IP address of your domain, but they know where to send the resolver to find the Top-Level Domain (TLD) server (e.g., .com, .org).
TLD Name servers. TLD name servers are the directory for domain extensions. These servers manage specific domain extensions (e.g., .com, .org, .net).They direct the resolver to the Authoritative Name Server for the specific domain
The final answer is Authoritative Name server. **This server holds the actual DNS records for the domain (e.g., example.com).**
It provides the IP address for the domain to the resolver, which then sends it back to your computer.

DNS Records (The Data)
DNS records are stored on Authoritative Name Servers.

These records include:

* A Record: Maps a domain to an IPv4 address.

* AAAA Record: Maps a domain to an IPv6 address.

* CNAME Record: Maps a domain to another domain (aliasing).

* MX Record: Specifies mail servers for email delivery.

## Where Are These Servers Physically Located?

* DNS servers are hosted in data centers all over the world.

* Companies like Google, Cloudflare, Amazon, and Akamai operate public DNS servers.

* Your ISP also runs its own DNS servers.

## How It All Works Together:
1. You type example.com in your browser.

2. Your computer asks the Recursive Resolver for the IP address.

3. The resolver queries the Root Server, which points it to the .com TLD Server.

4. The TLD Server points the resolver to the Authoritative Name Server for example.com.

5. The Authoritative Server provides the IP address (93.184.216.34).

The resolver sends the IP address back to your computer, and your browser loads the website.
