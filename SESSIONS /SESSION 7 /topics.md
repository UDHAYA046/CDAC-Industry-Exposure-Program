# Session 7 – Footprinting and Reconnaissance: Detailed Topic List

## 1. Footprinting Fundamentals
- Meaning of footprinting
- Footprinting as the first phase of attack or penetration testing
- Footprinting as information gathering
- Purpose: finding possible ways to intrude into a target network
- Attacker mindset during footprinting
- Ethical hacker mindset during footprinting
- Difference between attacker and penetration tester

## 2. Types of Footprinting
- Passive Footprinting
  - Gathering information without direct interaction
  - Public sources
  - Search engines
  - Social media
  - Breach databases
  - Job portals
- Active Footprinting
  - Gathering information with direct interaction
  - DNS queries
  - WHOIS lookup
  - Network probing
  - Traceroute
  - Subdomain enumeration

## 3. Information Obtained During Footprinting
### 3.1 Organization Information
- Employee details
- Telephone numbers
- Branch and location details
- Background of the organization
- Web technologies
- News articles
- Press releases
- Related public documents

### 3.2 Network Information
- Domains
- Subdomains
- Network blocks
- Network topology
- Trusted routers
- Firewalls
- IP addresses of reachable systems
- WHOIS records
- DNS records

### 3.3 System Information
- Web server operating system
- Location of web servers
- Publicly available email addresses
- Usernames
- Passwords leaked in breaches

## 4. Footprinting Threats
- Social engineering
- System attacks
- Network attacks
- Information leakage
- Privacy loss
- Corporate espionage
- Business loss

## 5. Footprinting Methodology
- Footprinting through search engines
- Footprinting through web services
- Footprinting through social networking sites
- Website footprinting
- Email footprinting
- WHOIS footprinting
- DNS footprinting
- Network footprinting
- Footprinting through social engineering

## 6. Footprinting Through Search Engines
- Using Google, Bing, Yahoo and other search engines
- Finding employee details
- Finding login pages
- Finding intranet portals
- Finding exposed documents
- Finding technology platforms
- Finding public reports
- Finding job portals
- Finding archived or cached pages

## 7. Advanced Google Hacking Techniques
- Google dorking
- Search operators
- Complex search queries
- Filtering search results
- Sorting specific target information

### Operators to Cover
- `site:`
- `inurl:`
- `allinurl:`
- `intitle:`
- `allintitle:`
- `inanchor:`
- `allinanchor:`
- `cache:`
- `link:`
- `related:`
- `info:`
- `location:`
- `filetype:`

## 8. Sensitive Information Found Through Google Hacking
- Error messages
- Files containing passwords
- Sensitive directories
- Login portals
- Network data
- Vulnerability data
- IDS logs
- Firewall logs
- Configuration files
- Server vulnerabilities
- Software version information
- Web application source code
- IoT control panels
- Hidden web pages
- Intranet pages
- VPN services

## 9. Google Hacking Database
- GHDB meaning
- Exploit Database connection
- Categories of Google dorks
- Footholds
- Username files
- Password files
- Sensitive directories
- Vulnerable files
- Vulnerable servers
- Error messages
- Juicy information
- Login portals
- Online devices
- Advisories and vulnerabilities

## 10. VPN Footprinting Through Google Hacking
- Finding VPN login portals
- SSL VPN pages
- Fortinet VPN pages
- OpenVPN configuration files
- Citrix Gateway portals
- Netscaler portals
- Cisco ASA login pages
- VPN configuration exposure
- OpenVPN static keys
- Sensitive VPN directories

## 11. Other Search Engine Footprinting Techniques
- Google Advanced Search
- Advanced Image Search
- Reverse Image Search
- Video Search Engines
- Meta Search Engines
- FTP Search Engines
- IoT Search Engines

## 12. Advanced Image Search
- Google Image Search
- TinEye Reverse Image Search
- Yahoo Image Search
- Bing Image Search
- Google Lens
- Finding original image sources
- Identifying reused profile photos
- Discovering locations through images
- Extracting contextual clues from images

## 13. Video Search Engine Footprinting
- YouTube
- Google Videos
- Yahoo Videos
- Bing Videos
- Video metadata
- YouTube Metadata
- YouTube DataViewer
- EZGif
- VideoReverser
- Extracting upload time
- Extracting channel details
- Extracting video thumbnails
- Converting video to text or frames

## 14. Meta Search Engine Footprinting
- Startpage
- MetaGer
- Privacy based searching
- Aggregated results
- Searching without direct Google tracking

## 15. FTP Search Engine Footprinting
- FTP search engines
- NAPALM FTP Indexer
- Finding open FTP directories
- Finding password files
- Finding logs
- Finding backup files
- Finding exposed documents
- Finding admin folders
- Finding FTP configuration files

## 16. IoT Search Engine Footprinting
- Shodan
- Censys
- Thingful
- Internet connected devices
- Routers
- Cameras
- Servers
- Printers
- IoT dashboards
- Open ports
- Device banners
- SSL certificate data
- Geographical exposure map

## 17. Finding Top Level Domains and Subdomains
- External URLs
- Company owned domains
- TLD discovery
- Subdomain discovery
- Department identification through subdomains
- Business unit identification
- Trial and error discovery
- Netcraft
- Sublist3r
- Pentest tools subdomain finder

### Subdomain Tool Options
- `-d` domain
- `-b` brute force
- `-p` ports
- `-v` verbose
- `-t` threads
- `-e` search engines
- `-o` output
- `-h` help

## 18. Social Networking Footprinting
- Facebook
- Twitter
- LinkedIn
- Employee information
- Location
- Emails
- Websites
- Blogs
- Contacts
- Important dates
- Personal interests
- Professional roles
- Social engineering preparation

## 19. People Search Services
- Spokeo
- Intelius
- Pipl
- BeenVerified
- Whitepages
- PeekYou
- Names
- Addresses
- Contact details
- Date of birth
- Photographs
- Videos
- Profession

## 20. Footprinting Through Job Sites
- Job requirements
- Employee profiles
- Hardware information
- Software information
- Cloud stack
- Security tools
- Server technologies
- Firewall products
- VPN products
- Operating systems
- Internal platforms

## 21. Deep Web and Dark Web Footprinting
- Deep web meaning
- Unindexed content
- Dark web meaning
- Anonymous browsing
- TOR Browser
- Freenet
- GNUnet
- I2P
- Retroshare
- Dark web marketplaces
- Leaked databases
- Credential dumps

## 22. Determining Operating System
- Shodan OS identification
- Censys exposed device information
- Banners
- Server headers
- Technology fingerprints
- Router and server discovery

## 23. VoIP and VPN Footprinting
- VoIP exposure
- VPN exposure
- Shodan filters
- Censys filters
- Routers
- VPN gateways
- SIP services
- Internet exposed devices

## 24. Footprinting Through Web Services
- Google Earth
- Google Finance
- Web services as public intelligence sources
- Physical location discovery
- Business information discovery
- Financial information discovery

## 25. Website Footprinting
- Browsing the target website
- Software used
- Software version
- OS used
- Scripting platform
- Subdirectories
- URL parameters
- File names
- Paths
- Database field names
- Query strings
- Technologies used
- Contact details
- CMS details

## 26. Website Mirroring
- Downloading a website locally
- Offline browsing
- Directory structure discovery
- Local analysis
- Reducing repeated requests to server
- HTTrack Website Copier
- Cyotek WebCopy
- HTML files
- Images
- Flash files
- Videos
- Other assets

## 27. Extracting Website Links
- Link extraction
- Octoparse
- Crawling website structure
- Finding hidden pages
- Finding URLs
- Finding forms
- Finding linked documents

## 28. Monitoring Web Pages for Updates and Changes
- Website update monitoring
- Aignes tools
- Contact information tracking
- Email address discovery
- Telephone number discovery
- Web page posting patterns
- Revision numbers
- Website traffic monitoring

## 29. Website Traffic Intelligence
- Total visitors
- Page views
- Bounce rate
- Live visitor map
- Site ranking
- Audience geography
- Visitor tracking
- Sales monitoring
- Tools:
  - Clicky
  - Opentracker
  - Google Analytics
  - Web Stat
  - Rank Tracker
  - GoingUp

## 30. Email Footprinting
- Email tracking
- Tracking delivery
- Recipient IP address
- Geolocation
- Browser details
- OS details
- Social engineering preparation
- EmailTrackerPro

## 31. WHOIS Lookup
- WHOIS databases
- Regional Internet Registries
- Domain owner information
- Registrar
- Domain creation date
- Expiry records
- Last updated records
- Name servers
- NetRange
- Contact details

## 32. Regional Internet Registries
- RIR concept
- ARIN
- RIPE NCC
- APNIC
- LACNIC
- AFRINIC
- IP allocation records
- Network ownership

## 33. IP Geolocation
- Country
- Region
- State
- City
- ZIP code
- Time zone
- Connection speed
- ISP
- Hosting company
- Domain name
- IDD country code
- Area code
- Mobile carrier
- Elevation
- IP2Location
- IP Location Finder

## 34. DNS Footprinting
- DNS records
- Server location
- Key hosts
- DNS interrogation
- SecurityTrails
- NSLOOKUP
- DNS Records tools

### DNS Records to Explain
- A record
- AAAA record
- MX record
- NS record
- TXT record
- CNAME record
- SOA record
- PTR record

## 35. Reverse DNS Lookup
- PTR records
- Mapping IP to hostname
- DNSRecon
- MXToolbox
- Reverse Lookup tools

## 36. Locating Network Range
- Target network mapping
- IP address ranges
- Subnet masks
- ARIN WHOIS
- RIR databases
- Public IP blocks
- Attack surface mapping

## 37. Traceroute
- Traceroute concept
- ICMP
- TTL field
- Router path discovery
- Hop by hop routing
- Network route mapping
- Latency observation

## 38. OSINT Framework
- OSINT meaning
- Free intelligence gathering tools
- OSINT tree structure
- Tool categories
- Indicator meanings:
  - T means local tool
  - D means Google Dork
  - R means registration required
  - M means manual URL editing required

## 39. Footprinting Countermeasures
- Restrict employee social media access
- Configure web servers to reduce leakage
- Educate employees to use pseudonyms
- Avoid critical information in press releases
- Avoid critical information in annual reports
- Avoid sensitive product catalogue exposure
- Limit information published online
- Discover and remove sensitive public information
- Prevent search engine caching
- Use anonymous domain registration
- Avoid domain level cross linking
- Encrypt sensitive information
- Password protect sensitive documents
- Disable unnecessary protocols
- Use TCP/IP filters
- Use IPsec filters
- Configure IIS securely
- Hide banner information
- Hide IP information through VPN or secure proxy
- Request archive.org removal
- Keep domain profile private
- Keep critical business documents offline

## 40. Practical Demonstrations To Include
- Have I Been Pwned email breach check
- Email breach history interpretation
- IndiaMART breach example
- Domino’s India breach example
- Medium article on external footprinting tools
- Dmitry tool reference
- WHOIS tool reference
- Google dork examples
- Shodan example
- Subdomain search examples
