# NextNote (alpha)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/brantje/nextnote/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/brantje/nextnote/?branch=master)   
This application is a rewritten verion of ownNote.<br>
The old [Android App](https://play.google.com/store/apps/details?id=com.nowsci.ownnote&hl=sv) won't work, but no worries, we plan to develop a new one.
    
Changes:
- Replaced deprecated methods
- Removed XSS vulnerability (Via the announcements it was possible to inject javascript / html)
- Updated tiny MCE to  4.6.4.
- Fixed CSP error in tinymce.
- Ability to embed files from your nextcloud 
- Ability to link to files from your nextcloud
- Make use of Entity's, mappers, services

## Pull requests are very welcome!
The whole app has been rebuild, so there will be some bugs in there.   
Did you found a bug? Report it or fix it and send a PR.

## Features
- Import from Evernote
- Full fledged WYSIWYG editor
- Share a note with a user or group
- Note grouping/categorization
- Archive notes


#Todo:
- [x] Refactor backend to make use of:
  - [x] Entity's
  - [x] Mappers
  - [x] Services
- [x] Switch to a AngularJS frontend
- [X] Rename namespace from OwnNotes to NextNotes
- [x] Implement note sharing
- [ ] Ability to save files to a folder as HTML files (untested)
- [ ] Implement hierarchical structure for groups (PR's welcome!)
- [ ] Add markdown support
- [ ] Import from [Notes](https://github.com/nextcloud/notes) app.
- [ ] Switch between database or file mode
- [ ] Add admin section for allowed image / video domains due CSP.
- [ ] Encrypted notes? (What about sharing?)
- [ ] Travis tests (We really need help with this, so PR's welcome!) 
- [ ] Develop an app for Android/iOS (We really need help with this, so PR's welcome!)
   
## Chat
There is a [Telegram](https://t.me/NextNote) chatroom available.
   
## Installation
- Place this app in **nextcloud/apps/nextnote** (Rename the extracted ZIP to "nextnote" or you will receive errors)
- Note: *custom_csp_policy* changes are no longer required

#### Scripted installation

You can also use this script developed by [enoch85](https://github.com/enoch85):
```
#!/bin/bash

pull() {
cd /var/www/nextcloud/apps || exit
rm -rf nextnote
git clone https://github.com/brantje/nextnote.git nextnote
chown -R www-data:www-data /var/www/nextcloud/apps/nextnote
sudo -u www-data php /var/www/nextcloud/occ app:enable nextnote
}

if pull
then
    exit
else
    echo "not sucessfull pull $(date)" > /var/scripts/pull.log
fi
```

Simply just run it everytime you want to get the latest master code.

## Development

NextNotes uses a single `.js` file for the templates.   
This gives the benefit that we don't need to request every template with XHR.
For CSS we use SASS so you need ruby and sass installed.
`templates.js` and the CSS are built with grunt, so don't edit them as your changes will be overwritten next time grunt is ran.   
To watch for changes use `grunt watch`
