<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- What a domain is
- What hosting is
- What an IP address is
- How to set up FileZilla
- How to upload files to FileZilla
- How to upload files with Netlify
- that there are other common hosting options like AWS, GCP and Heroku
-->

# FTP and domains

## Domains and hosting
We at Juno are all about promoting your online presence. Every developer needs a website to host their portfolio and a bit about them. When purchasing your website, it's important to understand the two main components of owning a website.

### Hosting
A _host_ is a server that holds the files your website that make up your website. Hosting servers can be located anywhere in the world, and most hosting is shared, which means that servers hold files for many users.

A _live_ website is one whose files are hosted on a server.

### Domain names
Each computer has an _internet protocol_ (IP) address. IP addresses are unique sets of numbers (e.g. `120.120.01.01`) that computers use to identify themselves. An IP address is like a computer's name.

It's easier for humans to remember words than numbers, so the _domain name system_ (DNS) points anyone who goes to <https://junocollege.com/> to `120.120.01.01`. Domain names are like IP addresses in human language.

Domain names can be purchased together with hosting or separately. When purchased separately, you need to tell the domain name system (DNS) that you want your domain name to point your hosting server's IP address. In these cases, you will need to ask your hosting company for which name servers to use. They usually look something like `ns1.hostingprovidername.com` and you should be able to find them in the settings where you bought your domain. If you're having trouble the domain and hosting companies are often more helpful than instructors, but feel free to reach out to both.

To learn more about how your browser connects to a website, check out [this cute and informative comic](https://howdns.works)! (The same people have a great comic on how [HTTPS works](https://howhttps.works/).)

## Domain and hosting providers

> **Disclosure:**
> Juno receives remuneration from the following companies when you use our affiliate links below. All proceeds we receive from affiliate partnerships are used for awesome alumni programming, such as Visibility:Hidden!

Domains:
* [Hover](https://hover.com/IbL8v5UV)
* [Namecheap](http://www.jdoqocy.com/click-8951841-11426545)

Hosting:
* [DreamHost](http://www.dreamhost.com/r.cgi?2137548)
* [SiteGround](https://www.siteground.com/index.htm?afcode=8d0b6cfbb3392c6083f2310e4d1ae00a)
* [GreenGeeks](https://www.greengeeks.com/track/hackeryou/cp-default)
* [HostGator](https://partners.hostgator.com/hackeryou)

Before you buy your domain and hosting, check out [this list of tips](https://github.com/HackerYou/bootcamp-notes/blob/master/stuff-you-need-to-know/resources-and-cheat-sheets/hosting-and-domain-tips.md).
## FTP

A _file transfer protocol_ (FTP) allows you to connect to your server so you can upload your website's files.

There are many, many ways to make this connection (e.g. Rails developers may use something called Capistrano or Heroku deployment tools) but FTP is the simplest and most common for front-end developers.

To use FTP, we need an FTP client. You may have a favourite FTP client already, and you are welcome to use it. [FileZilla](http://filezilla-project.org/download.php?type=client) is very popular and works with both Mac and Windows, while [Transmit](http://panic.com/transmit/) is Mac-only.

### FTP username and password
If you already have an FTP username and password, you can skip this step.

Otherwise:
1. Log into your hosting account and click 'FTP accounts'. You may find it in the main menu, however dashboards may vary across different hosting services: 
  ![GreenGeeks main menu](https://hychalknotes.s3.amazonaws.com/ftp-menu-screenshot-2019.png)

2. Go ahead and enter a new set of credentials. Make sure the directory is set to `public_html` and not a sub-directory.
  ![Form to create an FTP account](https://hychalknotes.s3.amazonaws.com/create-ftp-account-screenshot-2019.png)

3. Put your username and password somewhere safe. 
  * Hot tip: use a password manager. Some popular ones are [1Password](https://1password.com) and [LastPass](https://www.lastpass.com/).

#### Navigating dashboards on different hosting providers
This process above will look different on each hosting provider's dashboard. For example, here is how it would look on Dreamhost's dashboard. 

1. Log in to the Dreamhost Homepage.
![Dreamhost Homepage Login Screen](https://hychalknotes.s3.amazonaws.com/dreamhost1.png)

2. In the left side panel, find the user option and click on 'Manage Users'.
![Dreamhost Dashboard highlighting Manage Users option](https://hychalknotes.s3.amazonaws.com/dreamhost2.png)

3. Click on the Add New User button, or use this screen to change the password or user settings of your existing users. ![Dreamhost Users Dashboard](https://hychalknotes.s3.amazonaws.com/dreamhost3.png)

4. Fill out the Add New User form. Make sure that you choose the FTP account option rather than the SFTP account. ![Dreamhost Add New User Form](https://hychalknotes.s3.amazonaws.com/dreamhost4.png)


## Configuring FileZilla

1. Click the blue and green 'Site Manager' icon in the top left corner.  
  ![Site manager icon below the window's exit and minimize buttons](https://hychalknotes.s3.amazonaws.com/site-manager-icon-screenshot-2019.png) 
2. Click 'New Site' to enter your credentials.
  ![Site manager window in FileZilla](https://hychalknotes.s3.amazonaws.com/site-manager-config-screenshot-2019.png)
3. Rename 'New site' to whatever you like.
4. Host is `ftp.yourdomainname.com` (replace `yourdomainname` with your domain name).
5. Leave 'Port' and 'Protocol' as they are.
6. Change 'Encryption' to 'Only use plain FTP (insecure)'.
7. Set 'Logon Type' to 'Normal'.
8. User is whatever you just set plus `@yourdomainname.com` (e.g. `marissa@marissaodesign.com`)
9. Password is whatever you set.

Go ahead and click 'Connect' and you should connect to your server.

FileZilla will now show a listing of all the files on your **local** machine on the left side and all the files in the **root** directory of your **remote** web server on right side.

![FileZilla interface, showing local and remote directories](https://hychalknotes.s3.amazonaws.com/filezilla-local-and-remote-screenshot-2019.png)

You can navigate between the files and directories on both sides like a normal Explorer or Finder window. To upload to the server, drag and drop from the left side to the right side. 

The server works just like your computer: upload an `index.html` file and surf to `www.yourdomain.com` and you will see your `index.html`. (With some server configurations, you'll need to place your files in the `public_html` directory.) Similarly, you can upload a folder called `finalproject` and surf to `www.yourdomain.com/finalproject` to see it.

A best practice is to edit your website locally (on your computer) until you are happy with your progress. Then drag and drop the entire folder onto your server.

## Hosting Services
There are several other services that are commonly used to host more fullstack applications on the web, they include:

* Heroku
* Amazon Web Services (AWS)
* Google Cloud Platform (GCP)
* Microsoft Azure

Although these services offer more than we need in order to host a static website, you may end up interacting with them in your web development career as most companies will use a cloud hosting service to serve their product or website to their clients.

These services allow you to host a server that you build yourself. This is unlike a service like Dreamhost that has a server that exists somewhere on the internet where you upload your static files.

All of these services come with their own jargon and tools for interacting with them. Often, you will need to install a CLI tool (a tool that allows you to interact with the service from your command line) in order to get started. You can think of these services as a very basic operating system running on a computer that is hosted on the cloud. In order to run your app or website on these services, you need to fully setup your environment including installing any dependencies, setting up databases and running a server to serve the front end code.

Each company will have their own deployment process, often to deploy your code you will either have to push or merge your code into a specific branch on Github. For example, the `master` branch might hold all the code that the company is working on, while the `production` branch holds the code that is live on the web somewhere. In order to deploy code, you would need to make a pull request to the `production` branch.  

There is an entire subset of the web development community whose entire job is to work with these services and ensure that's web hosted platforms stay live called Developer Operations or Dev Ops.

## Using Netlify
Netlify is a tool that makes deploying and hosting a website very straightforward. It takes away the need to FTP into your server and add files manually. Instead, you add files you would like to be seen live on the internet through the Netlify web app.

When signing up for Netlify, it is easiest if you link your Github account directly to your Netlify account. The following steps assume that is how you have chosen to setup your account.

### Register a Domain
You can either purchase a domain through Netlify or use a domain you have purchased from another provider. In order to purchase a domain name through Netlify, follow the below steps:

1. Navigate to the 'Domains' tab
![](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202020-04-01%20at%2012.05.18%20PM.png)
2. Enter your domain and click 'Verify'
![](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202020-04-01%20at%2012.06.47%20PM.png)
3. If the domain is available, you will be prompted to purchase it! 

### Transfer a domain to Netlify
If you have already purchased a domain through another service you will need to transfer your name servers to Netlify. Your domain name registrar should have documentation on this called something along the lines of 'Changing your domain name server`. 

Here are the instructions for a couple of common domain registrars:
- [Hover](https://help.hover.com/hc/en-us/articles/217282477-How-to-Change-your-domain-name-servers-DNS-servers-Updated-March-2016-)
- [GoDaddy](https://ca.godaddy.com/help/change-nameservers-for-my-domains-664)


### Deploy with Netlify
Netlify has a 'drag and drop' deploy system that makes it very easy to get static sites live.

Simply navigate to the `sites` tab in your Netlify account and drag and drop the entire project folder into the part of the UI waiting to receive files. 
![](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202020-04-01%20at%202.11.21%20PM.png)

As long as there is an `index.html` file in the root of the folder, Netlify will deploy your site and display the randomly generated URL where your site is now live. 

You can also use Netlify's Github integration to deploy your sites from Github. In the same Sites tab, click the `New Site from Git` button and select Github. As long as you have signed up for Netlify through Github, Netlify will prompt you to further authorize your Github account with Netlify. Follow these steps, giving Netlify access to your Github repos.

Once Netlify is able to access your Github, you will be shown a list of your Github repos. Choose the one you wish to deploy and fill out the required fields. For a static site, you do not need a build command or a publish directory. For React sites using Webpack or another build tool, fill these fields out with the appropriate build command. For React apps using Create-React-App these fields should be filled in with: `npm run build` and `build`. 

Click the `Deploy` button and after a few seconds, Netlify should deploy your site to a random URL. 

Should you wish to add this project as a `subdomain` of your domain, you will be prompted to do so under the `Branch subdomains` section after you deploy your side. In order to gain access to this feature, you will need to have added your domain to Netlify.

### Creating Nested Routes
A nested route is any route on your main domain that is not just the domain itself. For example, your main domain might be `mybeautifulwebsite.com` and a nested route on that site would be `mybeautifulwebsite.com/project-one`.

 You can create nested routes by adding a plain text `_redirects` file to the site you are hosting on your main domain. This file would need to be structured as follows and be saved in the root directory alongside the `index.html` file.

Sample `_redirects` file:
```shell
/project-one        https://www.randomrandomnetlifyname.com
/project-two        https://www.equallyrandomnetlifyname.com
```
On the left are listed the various nested routes you would like your site to have and on the right are the randomly generated URLs where those sites are hosted. This could be github page links as well.

This file should be saved in the root of your project directory, below is a sample project directory:
```bash
- website(root folder)
    index.html
    _redirects
    script.js
    - styles
      style.css
      - assets
        imageOne.png
```