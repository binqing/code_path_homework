# Project 7 - WordPress Pen Testing

Time spent: 10 hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pen Testing Report

### 1. (Required) WordPress 4.0-4.7.2 - Authenticated Stored Cross-Site Scripting (XSS) in YouTube URL Embeds

- [ ] Summary: In WordPress before 4.7.3 (wp-includes/embed.php), there is authenticated Cross-Site Scripting (XSS) in YouTube URL Embeds.
               It llows an hacker to create random post on a site and store malicious Javascript code in it. The code will be executed when
               a visitor views the post and when someone edits the post from WordPress dashboard.
  - Vulnerability types: XSS
  - Tested in version: 4.2
  - Fixed in version: 4.2.13 
- [ ] GIF Walkthrough: <img src="YouTube-XSS.gif" alt="YouTube URL Embeds">
- [ ] Steps to recreate: 
   - 1. Log into WP as admin
   - 2. Create a new post 
   - 3. Edit as text and put: 
    - [ ] Here is the YouTube link: [embed src='http://youtube.com/embed/12345\x3csvg onload=alert(12345)\x3e'][/embed]     
- [ ] Affected source code:
  - [Affected source code](https://github.com/WordPress/WordPress/commit/419c8d97ce8df7d5004ee0b566bc5e095f0a6ca8)
- [ ] References:
  - [CVE-2017-6817](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-6817)
  - [Reference](https://core.trac.wordpress.org/browser/branches/4.1/src/wp-includes/class-wp-embed.php)

### 2. (Required) Vulnerability Name or ID

- [ ] Summary: 
  - Vulnerability types:
  - Tested in version: 4.2
  - Fixed in version: 
- [ ] GIF Walkthrough: 
- [ ] Steps to recreate: 
- [ ] Affected source code:
  - [Link 1](https://github.com/WordPress/WordPress/commit/419c8d97ce8df7d5004ee0b566bc5e095f0a6ca8)

### 3. (Required) Vulnerability Name or ID

- [ ] Summary: 
  - Vulnerability types:
  - Tested in version: 4.2
  - Fixed in version: 
- [ ] GIF Walkthrough: 
- [ ] Steps to recreate: 
- [ ] Affected source code:
  - [Affected source code](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)

### 4. (Optional) Vulnerability Name or ID

- [ ] Summary: 
  - Vulnerability types:
  - Tested in version:
  - Fixed in version: 
- [ ] GIF Walkthrough: 
- [ ] Steps to recreate: 
- [ ] Affected source code:
  - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)

### 5. (Optional) Vulnerability Name or ID

- [ ] Summary: 
  - Vulnerability types:
  - Tested in version: 4.2
  - Fixed in version: 
- [ ] GIF Walkthrough: 
- [ ] Steps to recreate: 
- [ ] Affected source code:
  - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php) 
  
### 6. (Optional) Vulnerability Name or ID

- [ ] Summary: 
  - Vulnerability types:
  - Tested in version: 4.2
  - Fixed in version: 
- [ ] GIF Walkthrough: 
- [ ] Steps to recreate: 
- [ ] Affected source code:
  - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php) 

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
