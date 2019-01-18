<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- What a domain is
- What hosting is
- What an IP address is
- How to set up FileZilla
- How to upload files to FileZilla
-->

# FTP and domains

## Domains and hosting
We at HackerYou are all about promoting your online presence. Every developer needs a website to host their portfolio and a bit about them. When purchasing your website, it's important to understand the two main components of owning a website.

### Hosting
A _host_ is a server that holds the files your website that make up your website. Hosting servers can be located anywhere in the world, and most hosting is shared, which means that servers hold files for many users.

A _live_ website is one whose files are hosted on a server.

### Domain names
Each computer has an _internet protocol_ (IP) address. IP addresses are unique sets of numbers (e.g. `120.120.01.01`) that computers use to identify themselves. An IP address is like a computer's name.

It's easier for humans to remember words than numbers, so the _domain name system_ (DNS) points anyone who goes to <https://hackeryou.com> to `120.120.01.01`. Domain names are like IP addresses in human language.

Domain names can be purchased together with hosting or separately. When purchased separately, you need to tell the domain name system (DNS) that you want your domain name to point your hosting server's IP address. In these cases, you will need to ask your hosting company for which name servers to use. They usually look something like `ns1.hostingprovidername.com` and you should be able to find them in the settings where you bought your domain. If you're having trouble the domain and hosting companies are often more helpful than instructors, but feel free to reach out to both.

To learn more about how your browser connects to a website, check out [this cute and informative comic](https://howdns.works)! (The same people have a great comic on how [HTTPS works](https://howhttps.works/).)

## Domain and hosting providers

> **Disclosure:**
> HackerYou receives remuneration from the following companies when you use our affiliate links below. All proceeds we receive from affiliate partnerships are used for awesome alumni programming, such as Visibility:Hidden!

Domains:
* [Hover](https://hover.com/IbL8v5UV)

Hosting:
* [DreamHost](http://www.dreamhost.com/r.cgi?2137548)
* [SiteGround](https://www.siteground.com/index.htm?afcode=8d0b6cfbb3392c6083f2310e4d1ae00a)
* [GreenGeeks](https://www.greengeeks.com/track/hackeryou/cp-default)
* [Bluehost](http://www.bluehost.com/track/hackeryou) 
* [HostGator](https://partners.hostgator.com/hackeryou)

## FTP

A _file transfer protocol_ (FTP) allows you to connect to your server so you can upload your website's files.

There are many, many ways to make this connection (e.g. Rails developers may use something called Capistrano or Heroku deployment tools) but FTP is the simplest and most common for front-end developers.

To use FTP, we need an FTP client. You may have a favourite FTP client already, and you are welcome to use it. [FileZilla](http://filezilla-project.org/download.php?type=client) is very popular and works with both Mac and Windows, while [Transmit](http://panic.com/transmit/) is Mac-only.

### FTP username and password
If you already have an FTP username and password, you can skip this step.

Otherwise:
1. Log into your hosting account and click 'FTP accounts': 
  * ![Yellow diamond icon representing FTP accounts page on hosting interface](http://wes.io/L96O/content)

2. Go ahead and enter a new set of credentials. Make sure the directory is set to `public_html` and not a sub-directory.
  ![Form to create an FTP account](http://wes.io/L88a/content)

3. Put your username and password somewhere safe. 
  * Hot tip: use a password manager. Some popular ones are [1Password](https://1password.com) and [LastPass](https://www.lastpass.com/).

## Configuring FileZilla

1. Click the blue and green 'Site Manager' icon in the top left corner. 
  * ![Site manager icon below the window's exit and minimize buttons](http://f.cl.ly/items/0i0K3B0S1e273V2u0M0S/Screen%20Shot%202014-01-22%20at%201.25.49%20PM.png) 
2. Click 'New Site' to enter your credentials.
   ![Site manager window in FileZilla](http://f.cl.ly/items/3Y0V093u08133f0b0G09/Screen%20Shot%202014-01-22%20at%201.37.16%20PM.png)
3. Rename 'New site' to whatever you like.
4. Host is `ftp.yourdomainname.com` (replace `yourdomainname` with your domain name).
5. Leave 'Port' and 'Protocol' as they are.
6. Change 'Encryption' to 'Only use plain FTP (insecure)'.
7. Set 'Logon Type' to 'Normal'.
8. User is whatever you just set plus `@yourdomainname.com` (e.g. `marissa@marissaodesign.com`)
9. Password is whatever you set.

Go ahead and click 'Connect' and you should connect to your server.

FileZilla will now show a listing of all the files on your **local** machine on the left side and all the files in the **root** directory of your **remote** web server on right side.

![FileZilla interface, showing local and remote directories](http://f.cl.ly/items/432X360I0h2T3H2Y1b24/Screen%20Shot%202014-01-22%20at%202.16.43%20PM.png)

You can navigate between the files and directories on both sides like a normal Explorer or Finder window. To upload to the server, drag and drop from the left side to the right side. 

The server works just like your computer: upload an `index.html` file and surf to `www.yourdomain.com` and you will see your `index.html`. (With some server configurations, you'll need to place your files in the `public_html` directory.) Similarly, you can upload a folder called `finalproject` and surf to `www.yourdomain.com/finalproject` to see it.

A best practice is to edit your website locally (on your computer) until you are happy with your progress. Then drag and drop the entire folder onto your server.