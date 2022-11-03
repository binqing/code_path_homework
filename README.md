# Project 7 - WordPress Pen Testing

Time spent: 10 hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pen Testing Report

### 1. (Required) WordPress 4.0-4.7.2 - Authenticated Stored Cross-Site Scripting (XSS) in YouTube URL Embeds

- [ ] Summary: In WordPress before 4.7.3 (wp-includes/embed.php), there is authenticated Cross-Site Scripting (XSS) in YouTube URL Embeds.
               It allows an hacker to create random post on a site and store malicious Javascript code in it. The code will be executed when
               a visitor views the post and when someone edits the post from WordPress dashboard.
  - Vulnerability types: XSS
  - Tested in version: 4.2
  - Fixed in version: 4.2.13 
- [ ] GIF Walkthrough: 

  - <img src= YouTube_XSS.gif/>
  
- [ ] Steps to recreate: 
   - 1. Log into WP as admin
   - 2. Create a new post 
   - 3. Edit as text and put: Here is the YouTube link: [embed src='http://youtube.com/embed/12345\x3csvg onload=alert(12345)\x3e'][/embed]     
- [ ] Affected source code:
  - [Affected source code](https://github.com/WordPress/WordPress/commit/419c8d97ce8df7d5004ee0b566bc5e095f0a6ca8)
  - [Affected source code](https://core.trac.wordpress.org/browser/branches/4.1/src/wp-includes/class-wp-embed.php)
- [ ] References:
  - [CVE-2017-6817](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-6817)
  - [Reference](https://blog.sucuri.net/2017/03/stored-xss-in-wordpress-core.html)
 
### 2. (Required) WordPress 2.5-4.6 - Authenticated Stored Cross-Site Scripting via Image Filename

- [ ] Summary: In WordPress before 4.6.1, the media_handle_upload function in wp-admin/includes/media.php has a Cross-Site Scripting (XSS) 
               vulnerability. It allows remote attackers to inject arbitrary web script or HTML by tricking an administrator into uploading 
               an image file that has a crafted filename.
  - Vulnerability types: XSS
  - Tested in version: 4.2
  - Fixed in version: 4.2.10
- [ ] GIF Walkthrough: 

  - <img src= xss_img_attachment.gif />
  
- [ ] Steps to recreate: 
   - 1. Log into WP as admin
   - 2. Create a new post and select insert media to upload a image 
   - 3. In attachment details, set the title of image to:


   	 -  <img src="a" onerror="alert(document.cookie)" /> 



   - 4. In attachment display settings, select Link to Attachment Page. Insert the image into post. Publish the post.
   - 5. Whenever the attachment file is loaded, xss exploited script will be triggered.
   
- [ ] Affected source code:
  - [Affected source code](https://github.com/WordPress/WordPress/commit/c9e60dab176635d4bfaaf431c0ea891e4726d6e0)
  - [Affected source code](https://core.trac.wordpress.org/browser/tags/4.2.2/src/wp-admin/includes/media.php)
- [ ] References:
  - [CVE-2016-7168](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-7168)
  - [Reference](https://sumofpwn.nl/advisory/2016/persistent_cross_site_scripting_vulnerability_in_wordpress_due_to_unsafe_processing_of_file_names.html) 

### 3. (Required) WordPress <= 4.2.2 - Authenticated Stored Cross-Site Scripting (XSS) in Creating New Post

- [ ] Summary: Cross-Site Scripting vulnerability in the text editor box allows remote hackers to inject malicious code into the content
               of a post if they want to create a new post. This post can be later read by others who visits the site and included in dynamic content. 
  - Vulnerability types: XSS
  - Tested in version: 4.2
  - Fixed in version: 4.2.3
- [ ] GIF Walkthrough:
  - <img src= XSS.gif />
  -
- [ ] Steps to recreate: 
   - 1. Log into WP as admin
   - 2. Create a new post
   - 3. Edit as text and put: <a href="[caption code=">]</a><a title=" onmouseover=alert(123) ">link</a>

- [ ] Affected source code:
  - [Affected source code](https://core.trac.wordpress.org/changeset/33359)
- [ ] References:
  - [CVE-2015-5622](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-5622)
  - [CVE-2015-5623](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-5623)
  - [Reference](https://klikki.fi/wordpress-core-stored-xss/)
  - [References](https://blog.sucuri.net/2017/09/stored-cross-site-scripting-vulnerability-in-wordpress-4-8-1.html)

### 4. (Optional) User Enumeration using WPScan

- [ ] Summary: For our WordPress version, different error messages are displayed when a non-existent username is used to log in or when an invalid password is entered
               for an existing user. Thus, we can determine whether or not a user account exists or not. It also does not limit log-in 
               attemps. We can use WPScan to enumerate all users in the database, including those who have never posted or contributed to a post.
  - Vulnerability types: User Enumeration 
  - Tested in version: 4.2
  - Fixed in version: Unpatched
- [ ] GIF Walkthrough:
  - <img src= user_enumeration.gif/>
  -
- [ ] Steps to recreate: 
   - 1. Open Kali linux terminal and run: "wpscan --url [INSERT_WORDPRESS_URL_NAME] --enumerate u"
           - For example: wpscan --url http://wpdistillery.vm --enumerate u 
- [ ] Affected source code:
  - [Affected source code](https://core.trac.wordpress.org/browser/branches/4.1/src/wp-login.php)
  - [Affected source code](https://github.com/WordPress/WordPress/blob/4.2-branch/wp-login.php)
- [ ] References:
  - [CVE-2009-2335](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2009-2335)
  - [Reference](https://www.wpwhitesecurity.com/wordpress-username-disclosure-vulnerability/)

### 5. (Optional) Enumerate WordPress user accounts and brute force passwords attack using WPScan

- [ ] Summary: Enumerating WordPress users is the first step in a brute force attack in order to gain access to a WordPress account. 
               Wordpressdoes not limit the number of login attempts, so we use WPScan. WPScan has the option to scan a target website 
               to retrieve a list of account names. We can also brute force root passwords using WPScan on Kali Linux. We could also 
               provide a wordlist, a list of common passowrds for wpscan to carry out the brute force password attack.  A example of a wordlist is rockyou-75.txt. 
  - Vulnerability types: Login Vulnerability
  - Tested in version: 4.2
  - Fixed in version: Unpatched
- [ ] GIF Walkthrough:
  - <img src= brute-force-password.gif/>
 
- [ ] Steps to recreate: 
  - If you want to get a specific user's password:
   - 1. Download the rockyou.txt dictionary fille.
   - 2. Open Kali linux terminal 
   - 3. To get the name of a specific userL run: wpscan --url http://wpdistillery.vm --enumerate u.
   - 4. Then run: wpscan --url http://wpdistillery.vm -P /home/kalizhe/Desktop/WebSecurity/rockyou-75.txt --usernames sophia.
        WPScan will return the password of username sophia's password. 
        
 - [ ] GIF Walkthrough:
  - <img src= brute_force_passwords.gif/>
  
- [ ] Steps to recreate:
  - To get password for all WordPress account users:
   - 1. Download the rockyou.txt dictionary fille.
   - 2. Open Kali linux terminal and run: 
	        wpscan --url http://wpdistillery.vm -P /home/kalizhe/Desktop/WebSecurity/rockyou-75.txt 
- [ ] Affected source code:
  - [Affected source code](https://github.com/WordPress/WordPress/blob/4.2-branch/wp-login.php)
- [ ] References:
  - [CVE-2009-2335](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2009-2335)
  - [Reference](https://www.wpwhitesecurity.com/strong-wordpress-passwords-wpscan/)


### 6. (Optional) WordPress <= 4.3 - Authenticated Shortcode Tags Cross-Site Scripting (XSS)
- [ ] Summary: WordPress versions 4.2 is vulnerable to a cross-site scripting vulnerability when processing shortcode tags. By taking advantage of 
WordPress' mishandling of unclosed HTML elements during processing of shortcode tags, this vulnerability allows remote attackers to inject arbitrary web script 
or HTML elements when creating or editing pages or posts.
  - Vulnerability types: XSS
  - Tested in version: 4.2
  - Fixed in version: 4.2.5
- [ ] GIF Walkthrough: 
  - <img src= xss_short_code.gif />
  -
- [ ] Steps to recreate: 
   - 1. Log into WP as admin
   - 2. Create a new post
   - 3. Edit as text and put the following: 
	Wanna A Suprise!!![caption width="2" caption='<a href="' ">]</a><a href="http://onMouseOver='alert(12345678910)'">CLICK ME!</a>
   
- [ ] Affected source code:
  - [Affected source code](https://core.trac.wordpress.org/browser/tags/4.2.2/src/wp-includes/shortcodes.php)
  - [Affected source code](https://github.com/WordPress/WordPress/commit/f72b21af23da6b6d54208e5c1d65ececdaa109c8)
- [ ] References:
  - [CVE-2015-5714](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-5714)
  - [Reference](https://blog.checkpoint.com/2015/09/15/finding-vulnerabilities-in-core-wordpress-a-bug-hunters-trilogy-part-iii-ultimatum/)
  - [Reference](https://blog.knownsec.com/2015/09/wordpress-vulnerability-analysis-cve-2015-5714-cve-2015-5715/)
 





## Assets

List any additional assets, such as scripts or files

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [ScreenToGif](https://www.screentogif.com/) 

## Notes

Describe any challenges encountered while doing the work

## License

    Copyright [yyyy] [name of copyright owner]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
