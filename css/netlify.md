# Using Netlify
Netlify is a tool that makes deploying and hosting a website very straightforward. It takes away the need to FTP into your server and add files. Instead you add files you would like to be seen live on the internet through the Netlify web app.

When signing up for Netlify, it is easiest if you link your Github account directly to your Netlify account. The following steps assume that is how you have chosen to setup your account.

## Register a Domain
You can either purchase a domain through Netlify or use a domain you have purchased from another provider. In order to purchase a domain name through Netlify, follow the below steps:

1. Navigate to the 'Domains' tab
![](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202020-04-01%20at%2012.05.18%20PM.png)
2. Enter your domain and click 'Verify'
![](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202020-04-01%20at%2012.05.18%20PM.png)
3. If the domain is available, you will be prompted to purchase it! 

### Transfer a domain to Netlify
If you have already purchased a domain through another service you will need to transfer your name servers to Netlify. Your domain name registrar should have documentation on this called something along the lines of 'Changing your domain name server`. 

Here are the instructions for a couple common domain registrars:
- [Hover](https://help.hover.com/hc/en-us/articles/217282477-How-to-Change-your-domain-name-servers-DNS-servers-Updated-March-2016-)
- [GoDaddy](https://ca.godaddy.com/help/change-nameservers-for-my-domains-664)


## Deploy with Netlify
Netlify has a 'drag and drop' deploy system that makes it very easy to get static sites live.

Simply navigate to the `sites` tab in your Netlify account and drag and drop the entire project folder into the part of the UI waiting to receive files. 
![](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202020-04-01%20at%202.11.21%20PM.png)

As long as there is an `index.html` file in the root of the folder, Netlify will deploy your site and display the randomly generated URL where your site is now live. 

You can also use Netlify's Github integration to deploy your sites from Github. In the same Sites tab, click the `New Site from Git` button and select Github. As long as you have signed up for Netlify through Github, Netlify will prompt you to further authorize your Github account with Netlify. Follow these steps, giving Netlify access to your Github repos.

Once Netlify is able to access your Github, you will be shown a list of your Github repos. Choose the one you wish to deploy and fill out the required fields. For a static site, you do not need a build command or a publish directory. For React sites using Webpack or another build tool, fill these fields out with the appropriate build command. For React apps using Create-React-App these fields should be filled in with: `npm run build` and `build`. 

Click the `Deploy` button and after a few seconds, Netlify should deploy your site to a random URL. 

Should you wish to add this project as a `subdomain` of your domain, you will be prompted to do so under the `Branch subdomains` section after you deploy your side. In order to gain access to this feature, you will need to have added your domain to Netlify.

## Creating Subdomains
As was mentioned above, you can create subdomains for your projects on your custom domain that has been attached to Netlify. A subdomain is any route on your main domain that is not just the domain itself. For example, your main domain might be `mybeautifulwebsite.com` and a subdomain on that site would be `mybeautifulwebsite.com/project-one`.

You can create subdomains either through the `Settings` tab for a given site hosted on Netlify. Or by adding a plain text `_redirects` file to the site you are hosting on your main domain. This file might look something like this and be saved in the root directory alongside the `index.html`:

```shell
/project-one        https://www.randomrandomnetlifyname.com
/project-two        https://www.equallyrandomnetlifyname.com
```