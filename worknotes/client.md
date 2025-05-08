#### 5/7/25; 4:34:32 PM by DW

The first time a user publishes a post, show a dialog offering them a chance to view it on the web. This helps the newbie understand what just happened. 

The feature is written up <a href="https://this.how/wordland/dialogForPublish.opml">here</a>. 

Stopped the spinner when saving resulted in an error. Otherwise it would keep spinning forever.

#### 5/5/25; 10:09:28 AM by DW

Have to back out of the Styles panel of the Settings command, I did it way too fast, each feature it added had to be tested in this very particular context. 

The context is Medium Editor, Markdown and WordPress. None of which were designed to work with each other. We're lucky to have a core subset that works, enough to support writers.

I think to get a really complete editor, you have to start with Markdown or HTML and work it out with WordPress. 

I have made the style of H3 agree with the style of in the Baseline theme. 

So here's what I'm doing.

1. Removing the Styles panel in Settings (I'll save it in the source.opml file).

2. Add H3 to the non-configurable menu, since we now have end-to-end support.

#### 4/23/25; 2:49:01 PM by DW

Allow the user to change the operations in the popup text menu.

#### 4/20/25; 8:51:37 AM by DW

Changes make it possible to load in FeedLand posts in a WordLand timeline and for the timeline to be displayed outside a modal dialog. 

I'll be looking for an application for this, to get started on introducing the timeline for an RSS-only social web app.

#### 4/16/25; 11:34:21 AM by DW

When you set the version number you must set it in two places. I want it to be correct even if the JS doesn't run properly at startup. 

* appConsts.version

* in the html source at .divWordlandVersionNumber

#### 4/14/25; 8:58:18 AM by DW

Bookmarks menu is now optional, controlled by a setting, defaults false

* I want to go in the direction of the timeline.

* There is a bug in there, it also shows up in FeedLand, where the menu is emptied out. Someday I have to go in there, roll my sleeves up and find the problem. So that's another reason, it doesn't really work. But if people have been using it and like it, they can continue.

Editor notifies timeline of update to a draft. 

* Not just on publish, on any change that would cause the draft display in the timeline to change. 

Should a click anywhere in a draft expand the body, or just a click in the body.

* The problem comes up when you click the edit icon. Since its part of the draftviewer, it will expand the body, before it confirms you want to edit.

I think it has to be just a click on the body. Makes the code much more manageable. And you definitely don't want it expanding when you click the edit icon.

I'm back!

* I've been working on the side on the Timeline feature for WordLand. Actually it's more general, it should be able to fit into a bunch of slots. But for now it's a single command off the main menu that opens up your timeline of WordLand drafts. 

* I'm going to start making notes here about changes that relate to timelines, esp as integrated with WL.

#### 4/13/25; 12:00:52 PM by DW

In timeline, should a click anywhere in a draft expand the body, or just a click in the body.

The problem comes up when you click the edit icon. Since its part of the draftviewer, it will expand the body, before it confirms you want to edit.

I think it has to be just a click on the body. Makes the code much more manageable. And you definitely don't want it expanding when you click the edit icon.

#### 3/26/25; 10:36:31 AM by DW

New uploadImageCommand in the context menu. 

The one in the main menu will stay for a few days, while we check out this new place.

#### 3/23/25; 9:02:45 AM by DW -- how to release a new version of wordland

wordland.social vs wordland.dev

* wordland.social is the current public version, it gets the source code from http://scripting.com/code/wordland/

* it's running on the "peabody" server.

* wordland.dev is the next version, being developed, it gets its source from http://scripting.com/code/wordland/dev/

* it's running on the "maine" server.

To release a new version

* Change the version number in config.json on wordland.social. (It's running on utica.) (note i'm not doing this anymore, 5/5/25 by DW)

* Relaunch wordland.js on wordland.social.  

* Before doing so npm update if there were changes to packages it uses.

( wpidentity which is the server package, is updated automatically as the code changes.

* Change the version in appConsts in code.js and in index2.html (displayed in the menubar)

* Change the heading at the top of this outline to http://scripting.com/code/wordland/ and click Save button.

* Open up wordland.social and test. 

* Sign off and on. Create a new post. Do a reasonable amount of editing. Review the new features. 

* Update wpidentity and wordland repos on github, if necessary.

To change back to dev version

* Change the version number in config.json on wordland.dev, and in the scripting.com-code-wpidentityshell subfolder of the nodeEditor folder on local machine.

* Change the heading at the top of this outline to http://scripting.com/code/wordland/dev/ and click Save button.

* Restart the local test server and access it in the browser at localhost:1408.

#### 3/22/25; 8:50:30 AM by DW -- v0.51

New commands:

* setFeaturedImageCommand

* setExcerptCommand

New signon screen

* Links to the fact sheet for the product.

* Says Welcome to WordLand!

#### 3/22/25; 10:22:09 AM by DW

new commands in the context menu -- 

set excerpt

set featured image

set excerpt is just a dialog and setting a new property of a draft

the hard part is factoring the image uploading code so it can be told to use a specific blog, and to just return the id, not the html for the image.

#### 3/15/25; 6:04:54 PM by DW

New features in categories, written up in this <a href="https://github.com/scripting/wordlandSupport/issues/59">change note</a>.

#### 3/14/25; 10:20:28 AM by DW -- how to release a new version of wordland

To release a new version

* Change the version number in config.json on wordland.social (it's on peabody).

* Restart the server.

* Change the heading at the top of this outline to http://scripting.com/code/wordland/ and click Save button.

* Open up wordland.social and test. 

* Sign off and on. Create a new post. Do a reasonable amount of editing. Review the new features. 

To change back to dev version

* Change the version number in config.json on wordland.dev, and in the scripting.com-code-wpidentityshell subfolder of the nodeEditor folder on local machine.

* Change the heading at the top of this outline to http://scripting.com/code/wordland/dev/ and click Save button.

* Restart the local test server and access it in the browser at localhost:1408.

The new "dev" version of wordland on test.wordland.social.

Change the top heading in this project to /scripting.com/code/wordland/dev/

New macro: [%wordlandVersionString%] -- on test.wordland.social its value is "/dev", and on wordland.social it's ""

The macro is used in includes in the head section of index.html that reference files in this project. 

When you want to release a new version, change the top heading in this project to /scripting.com/code/wordland/.

Make sure it works, and then switch it back. 

Also, changed the home page from index.html to index2.html, so that we don't have to change anything in wordland.social right now. 

When we're ready to do the first switchover, we'll need to change the value of urlServerHomePageSource in its config.json.

#### 3/13/25; 11:09:39 AM by DW

I need to be able to work on the code of wordland without impacting the people using the deployed version. 



#### 3/3/25; 5:06:03 PM by DW

Tuning up using WordLand as an external editor.

* Allow the caller to specify the title of the post, and fill in the title editor with that string.

* Learned about giving an app a name which you can then use in calls to window.open. This makes it so that instances of WordLand can be reused. 

Defined clickInMainEditor function. Use it when you want to make sure the main edit box has the focus. 

#### 3/1/25; 12:01:12 PM by DW

Got tab key to work between the title editor and the main edit box. 

Removed the full selection of the text in the title editor. I never gave it a lot of thought, but I find it irritating. 

I move the cursor to the end of the text for teh title editor, considered doing the same for the main editor, but it already has some hairy code for handling clicks with the mouse. That's a hole I don't want to dig now. ;-)

#### 2/28/25; 10:44:18 AM by DW

I'd like to get markdown mode to work.

* when you click on the markdown icon, it should resize the text area after the switch

* when you reload a draft that's in markdown mode the text gets screwed up. looks like newlines are missing?

Cosmetic changes on the recent posts and recent users tables.

#### 2/22/25; 10:13:26 AM by DW -- how to debug wordland

It's on the peabody server, the name of the app is wordland.social. 

It's confusing because there are a lot of other similarly named apps in the pp listing on peabody.

At some point let's move wordland to another server, so that confusion is eliminated.

#### 2/6/25; 5:10:51 PM by DW

I keep losing my bookmarks. I want to get to the bottom of it. So I changed the way the call to myWordpress.readUserDataFile works. 

Previously if it couldn't read the bookmarks it would initialize it to an empty outline. Terrible choice. 

Now it puts up a very conspicuous alert dialog and when you click OK it reloads the page to try again. We're not going to let you lose your data, no matter what. We hope. :-)

You might look at the server and see if there are any errors in the console. 

#### 1/18/25; 11:05:53 AM by DW

We now handle app params, as are received from Bingeworthy when the user clicked on the button for a program. They will write or edit a review for that program, and coordinate with Bingeworthy so it knows how to display it and store it in its database. 

Look for "appParams" in code.js.

#### 1/4/25; 5:22:02 PM by DW

It was reported that when you accidentally double-click on the paper airplane icon you get two blog posts. 

Added a new global, whenPublishStart, if it's less than 3 seconds when we start a publish, we just beep the speaker and return. 

#### 1/2/25; 11:09:48 AM by DW

Changed the default on flAudibleIconClicks to false. I had it turned off almost immediately and forgot it defaults on for new users. 

#### 12/26/24; 10:25:36 AM by DW

Finished topUsersDialog, also wrote a runModalDialog function that I've wished I'd had for years. Now I have to remember to use it and where I put it. ;-)

#### 12/21/24; 10:30:29 AM by DW

Added audible clicks when the user clicks on an icon. Not sure I like it. 

#### 12/19/24; 10:30:51 AM by DW

After creating a new post, in the lower left corner instead of saying Draft, we say Choose a site. Click on it and you get to set the site for this post. You can get that out of the way when you're creating the post, or not -- if you want to get directly to writing. 

Now it says PUBLISHING in the status area between the time you click the paper airplane icon and the speaker beeps when it's done. I needed visual feedback there. 

Tried to get the autoLink feature working, both by turning the option on when creating the MediumEditor object and by writing my own code with the help of ChatGPT. Neither worked sufficiently so I commented out the code. 

#### 12/16/24; 9:38:33 AM by DW

Replaced the dialog where you choose which website to publish your draft to. 

Previously, we called currentWebsiteDialog from 

* publishCommand which is invoked when the user clicks on the airplane icon 

* newPostCommand when user chooses command from menu (but confusingly only if it's the first time you're choosing the command. this is vestigial, an old feature I never remembered to take out. going to have to think about this).

* uploadImageCommand when user chooses command from menu

It sets appPrefs.idLastSiteChosen, and it returns it as the second param to the callback

#### 11/14/24; 10:44:45 AM by DW

Upload image command in the main menu.

Prompt asks what wordpress site you want to upload the image to.

The command is in the new main menu.

Also removed the upload image and upload podcast commands from the context menu.

#### 11/13/24; 6:05:02 PM by DW

Back after a long hiatus for the election. 

It only took three days of intense bullshit to get image uploading working.

How it works -- choose a command from the menu, it prompts you to choose an image from a local file. 

It is uploaded to a wordpress site you choose. 

The htmltext for the image is put on the clipboard.

You can then paste it wherever you like. 

Still a bit of finishing work to do tomorrow.

A little <a href="https://daveverse.wordpress.com/2024/11/13/this-is-a-test-of-images/">demo</a>.

#### 11/4/24; 10:55:11 AM by DW

The Edit bookmark command in the side menu now opens the bookmarks editor with the cursor on the bookmark for the current post.

Look at afterOpen in editBookmarksCommand.

Changed some commands in the Tools menu. 

Enabled new plus icon.

Enabling left and right arrows.

#### 11/3/24; 11:46:49 AM by DW

Added a + icon to the icon line, and thus eliminated the need for the Menu at the top of the screen. It was the last remaining command.

There's a new pref, appPrefs.flConfirmNewPost, and you can change it in the Settings command. 

I wanted the area where you write the text of the post to be current when you create a new post, but not when you're looping through the posts, or choosing one from the bookmarks menu. So I added a new optional parameter to editDraft that determines whether we make it current, defaults to false, and pass it as true when clicking on the + sign.

#### 11/2/24; 12:30:40 PM by DW

We now use the array to implemented yesterday the left and right arrows in the text box. 

When wordland booted up, it would show the previous draft, then switch to the latest draft. this is because editDraft tried to rebuild the bookmarks menu and it didn't exist yet. that caused an error. the chatlog code was interpreting it as an error in opening the draft, which had been properly opened. Solved by checking to see if the menu had been built before rebuilding it. 

#### 11/1/24; 10:34:59 AM by DW

myWordpress.getNextPrevArray () -- returns an array of id's of the user's drafts. 

* we could reimplement the arrows so they don't require a hit to find the next or prev

* but this isn't done yet.

When we delete a draft, it is now also deleted from the Bookmarks menu.

The checkmark in the Bookmarks menu should now be correct when you click either of the arrows.

rewrote deletePostCommand. 

* Delete the draft first. If that works, delete the WordPress post. 

* You want to find out if there's a problem deleting the draft before going ahead and deleting the WordPress post. 

* If deleting the draft fails, we put up a dialog and do nothing more. 

* If deleting the WP file fails, we don't put up a dialog, display the error message in the console.

* The reason we don't put up a dialog is that we're going to change the display after the user clicks OK. 

* I would ignore the message as a user and click OK because I want to get on with it. 

#### 10/31/24; 10:38:06 AM by DW

Removed <i>Set current website</i> command. Since we ask for the website when we first publish a post, there's no need to set this. The default website should become the last one you selected. 

Moved <i>Get user info</i> command from the main menu to the system menu (the one all the way to the right).

Rebuilt bookmarks from database, new command in the Tools menu. In case you mess it up, you can start fresh. 

* Or if there's a bug that causes you to lose your bookmarks. 

* This happened to me the other day. I have no idea if there is some kind of bug or what. 

Spell out "Bookmarks" in the name of the Bookmarks menu. Later if we need the space we can abbreviate the name. It's a very important feature and there's lots of room in the menubar. 

Made more room for icons. The other side of the line is where you enter the title, but it scrolls as needed when typing. Very long titles might be a bit awkard, but I want those icons to feel comfortable, not cramped. divRightCell width changes from 170 to 200.

Moved RSS icon into the local menu to free up space. 

Tuned up the bottom message line. Previously every segment of the message had the same space. So "24 words" gets as much space as "Cats: User Interface". Now each item gets as much space as it needs, and what's constant is the spacing between them. This means we can probably add one or two more elements? But it's more rational.

#### 10/30/24; 1:04:04 PM by DW

Instead of counting characters, we now count words. Much more of a writer's thing. 

Added the user's name in a menu to the right edge of the menubar, with a command underneath that gets settings. This is the same UI as in Drummer and FeedLand. 

Changed "Save" to "Backup" in Tools menu.

#### 10/29/24; 12:48:41 PM by DW

Big changes in how bookmarks work. We manage them chronologically, by month. When we add a new draft, it goes at the top of the list for the month it was posted in. If the month doesn't exist, we create it. But you can reorganize, to have the items appear in different sections that you define. 

New Tools menu with three commands.

* VIew bookmarks OPML

* Save bookmarks OPML 

* Save drafts JSON

When there are no categories for a post, the status line just says <i>No Categories,</i> not <i>Cats: No cats</i>. It's more civilized, less digital. 

Removed commands from the main menu that are duplicated in the edit box.

Arrows in edit box for get next and prev drafts, it should be easy to scroll through the posts.  

Notes are <a href="https://github.com/scripting/wordlandSupport/issues/3">here</a>. 

#### 10/26/24; 9:22:22 AM by DW

Tested for the first time with a new user, one who had never used WordLand before. 

* A few little fixes needed, like don't assume when you ask for recent posts that the array will contain anything.

* But much more significant was that there was code in the chatlog object to create a new post, it wasn't up to date. We were editing new posts assuming that there already was a chatlog object set up. That required restructuring of the code and eliminating the duplicate functionality, basically simplifying everything, and also adding the functionality of creating a new empty unsaved post when you delete a post. 

Started the <a href="https://github.com/scripting/wordlandSupport">wordlandSupport repo</a>, public. 

#### 10/25/24; 1:40:17 PM by DW

Learned something about contenteditable objects. I was saving changes to the title, which is a contenteditable object, after a second of no typing, but i was always one character off in what I saved. Just noticed that today (why not sooner, I don't know). The problem was I was saving the element on "keydown" when I should have been saving on an "input" event. Thanks to <a href="https://chatgpt.com/share/671bd88b-bb2c-8012-b5e3-261ef877266d">ChatGPT</a>, my jQuery tutor. :-)

#### 10/21/24; 10:10:22 AM by DW

Fix up the display of categories in the status line.

* Use the name of the category instead of the slug.

* Put the full list of categories in the tooltip, so you don't have to click to see the dialog. 

Test the categories stuff with a new unpublished post



draftInfo.flTextChanged ==> draftInfo.flEnablePublish

* It used to be the only way you could enable publishing was by chaging the body text or title.

* But now you can do it by changing the categories, which is not the text changing. 

* So I changed the name to reflect its purpose. Don't want to introduce confusing hacks until we have to. ;-)

No need to work around "uncategorized" category. The server doesn't return it as part of the list of categories defined by the site. 

* It's not a choice I want to offer users, it's confusing. 

* Not sure how WordPress will work with this, we'll find out. 

Removed the users name as the first item on the status line

* how many users need to know their own name?

* you can get the same info from a command in the menu

#### 10/20/24; 6:49:10 PM by DW

I have categories user interface and saving and restoring working, with a couple of exceptions

* when we display the categories for the user we should always use the name, not the slug

* now in the status line we're using the slug because we don't have the full info marshalled

#### 10/19/24; 12:22:33 PM by DW

In getFeedXml, if the contentType of an item is markdown, for the description element, first convert it to HTML.

When you publish a post for the first time, the name of the site changes from Draft to the actual name in the status line. It's actually updated on every change, so it will always reflect the name of the site after you publish.

When the title changes, the airplane is be enabled.

source:markdown was appearing twice in the feed.

I was concerned that unpublished posts would appear in the feed, but we publish a feed for a specific site. Unpublished drafts don't have an idSite value, so they won't be returned by getRecentUserDrafts.

#### 10/18/24; 10:12:29 AM by DW

Working on the status line, the line at the bottom of the message display.

* Added a new entry, the second element, after the user's name -- the site the post came from, if it has been published. If it hasn't been published there's a message: "Not published." The tooltip contains the description of the site.

* The third element says when the post was created. It now shows the number of chars up to 512, after that it shows the number of K, or MB or even GB if posts ever get that big.  

In activateToolTips, i do the updating after a timeout of 5 milliseconds. I find under some circumstances some of the tool tips don't get activated. This is intended to make it more forgiving. 

The first time you publish a post, the dialog for choosing a site appears. 

* But only if you have confirmation dialogs enabled, appPrefs.flConfirmPublish.

* Otherwise I would be confused by which site the post is being published to. Since you can't change this once the post has been published, it should be clear.  

* So, when you click on the airplane for the first time for a post, the choose a site dialog pops up, if you don't have the feature turned off (it defaults on). 

#### 10/17/24; 11:30:53 AM by DW

After the user clicks OK in settings, reload the page, so the settings can take effect immediately.

I'm adding a pref that says whether the Markdown and Code icons are displayed, they default off. I don't trust them, too many quirks, and don't want to turn it over to users until it's supportable. In the U the commands will be marked experimental.

When you start up, what if appPrefs.idLastDraft points to something that has been deleted? We fall back, and ask the server for a list of recent drafts, and use the first in the list, that's the one we present the user with. 

Tool tip for title editor. (Decided not to do it. The object is actually a lot wider than the text (room to grow) so the tip shows up in a weird place. Not sure I want to fix it, and in the end it's kind of obvious without it.)

When you edit the title of a post, when you click off the title, it was saved before, but the airplane icon wasn't being enabled. This is because we were immediately saving the draft to the server to set the title, not going through the same process that happens when we're writing in the body of the post. Now we mark the draft as changed, and you can follow the progress in the saved status indicator in the right corner of the line below the edit box.

When you create a new post, you edit the title, add some text, then reload the page, the editor doesn't show the draft you created. Changed saveDraft so that if appPrefs.idLastDraft is different from the id of the draft just saved, we change appPrefs.idLastDraft and mark the prefs as changed, so they get updated in a second or two. Nice to get this bug fixed. ;-)

#### 10/14/24; 12:41:30 PM by DW

We now display the user's file list below the edit box. Code cribbed from an earlier version. 

It all works. 

Two new files contain the code and styles: files.js and files.css.

Note: to delete a file click on it in the list, and then choose the Delete command in the menu. 

#### 10/13/24; 10:59:11 AM by DW

Worked out the loose ends in the title editing function. It feels like perfection now, but of course there could still be problems.

We were still saving the draft as HTML after publishing. Changed publishDraft so it works with a copy of draftInfo, so it can't screw up the format, before the draft gets saved. 

I resurrected the Markdown icon, made it possible for both it and the Code icon to be there at the same time. Neither are imho too useful, but they broadcast the idea that we allow you to edit the text as Markdown or HTML, but fully expect people to stay with wizzy. And there are problems in using Markdown -- the code that translates between MD and HTML/Wizzy neutralizes Markdown when it shouldn't. I understand why they do it, it assumes when you were writing and not in MD mode, you don't want your chars to be interpreted as MD. But that means the text changes when you toggle between the two. That isn't right. We will figure out how to deal with this or possibly punt on the feature.

#### 10/12/24; 10:33:15 AM by DW

I made it so the title of the post is editable in place. 

* hated clicking to pop up a dialog.

* the command in the sidebar menu still pops up the dialog, should still work

I'm going to have to take out the </> icon, because it was never that useful, and now any HTML you enter will get stripped out in the conversion to and from Markdown. 

* I want to try using the Markdown icon and see if that can be made to work. This is the time to do it. 

* I left the </> icon in for now, because it actually seems to work! amazing -- probably are problems, but testing will prove or disprove

#### 10/12/24; 10:02:02 AM by DW

We now store the contents of the edit buffer in markdown, both in the draftInfo record attached to the document, and in the database on the server. 

We convert it to html as we're saving or updating the post on wordpress. But the local copy we keep remains in markdown. 

We noticed spans being added by MediumEditor or the OS, it isn't clear from the discussion thread on the mediumeditor repo. I tried writing code to strip out the spans it was known to add, but it didn't work well, was hard to debug, and while I was working on it didn't think it really solved the problem, so punted. 

The better way to proceed imho is to just strip out all spans, until we really get to the bottom of wtf is going on. But we're not doing that until we understand what's going on.

#### 10/10/24; 10:35:40 AM by DW

Trying out storing the the text of each post in markdown instead of html. 

Look for appConsts.flSaveAsMarkdown in the code. 

When we convert from html to markdown, it escapes all the markdown text we entered.

* I wrote code to neuter the escapes, but then there was no way to edit the markdown, so if you entered the wrong size title, there's no way in the current setup to fix it.

* So this will have to wait until we have a markdown button in the editor. 

There's still a problem 

When I publish, it doesn't convert the content to markdown, which coincidentally is exactly what WordPress is expecting. 

Probably the right thing to do is this -- 

1. save the text as markdown as all other situations

2. render the markdown before publishing, on the server side

But i want to take a break before doing that. think about it a bit. 



#### 10/9/24; 9:45:14 AM by DW

the mediumeditor package keeps adding <span>s to the text, this is annoying. adding code to remove any spans from the 

#### 10/8/24; 12:57:12 PM by DW

Added a Settings command, and settings.opml.

New pref, flConfirmPublish. 

I don't want to force a confirmation, but i want first time users to know what's happening. 

#### 8/2/24; 1:39:53 PM by DW

not going to do this right now, my mind is elsewhere, sorry.

i was doing a weeklong project to factor the editor out of this world, and create something standalone, but 

we still use chatlogs

i looked around for the new factored version, but didn't find it. 





factoring

i want wordland to be an editor that could be used with any identity and storage system

i do not want it to be dependent on wordpress, because i want it to be simpler, require less setup, and avoid support issues

i want a simpler product to support, however i want the current wordpress-based product to use it, so the codebase doesn't split

i'm doing this by copying the original wordland home project, and doing the factoring, so we have a standalone editor too that doesn't depend on wordpress



current structure

divChatlogContainer

divChatlog

divChatItem

divChatText

divChatText should be moved out of that structure and name changed to divWordLand

it has three items under it

divTopMsgLine

divMsgText

divBottomMsgLine

instead of <i>new chatlog</i> you say <i>new wordLand</i>

#### 6/3/24; 10:11:59 AM by DW

A corner-turn

chatlog, instead of managing a list of chatlogItem's will just manage one chatlogItem.

and the chatlogItem won't have an icon, it won't be a table, it'll just be a div

this will wreak havoc on the code. so we're moving away from the idea of a list of posts on screen to relying on the bookmarks to manage the list for us.

you won't be able to see two items on screen at the same time.

maybe an improvement down the road could be to add tabs, so you can at least switch between posts.

This is the structure we're managing now

divChatItemContainer

divChatItem

divTopMsgLine

divMsgText

#### 6/2/24; 9:50:33 AM by DW

Why you can't put an edit mode command in the popup menu.

clicking on the menu icon cause you to exit the editor

so while you're finding the command to switch the mode of the editor, the editor itself is gone

a moment of total confusion and just doesn't make sense

#### 5/31/24; 10:24:54 AM by DW

Bookmarks menu finally works, <a href="https://techfightclub.wpcomstaging.com/2024/05/31/two-concords-is-one-too-many/">found the problem</a> that caused doubled-up outline items when you press return. 

#### 5/30/24; 9:07:03 AM by DW

Had to provide a special ping url that calls rsscloud.io with https, so we can run WordLand on https.

#### 5/29/24; 11:40:33 AM by DW

i've got the bookmarks menu working.

the editor has a problem with return keys and you have to relaunch the main screen after opening the editor

when you choose a menu item, we pass the idDraft value to the chatlog, it removes the item if it's already in the list, and inserts it at the top

so you can have as many open documents as you want. 

next up -- closeboxes ;-)

#### 5/22/24; 10:46:01 AM by DW

if there is no title, just put the date

if there is a title -- you can leave out the "by Bull Mancuso" bit and go straight to the date

the idea is to take out unimportant distracting information and focus the attention on the text they wrote

#### 5/15/24; 11:48:02 AM by DW

We can now switch between modes on any message between wizzy, html or markdown editors.

#### 5/8/24; 11:17:56 AM by DW

Add menu command to set the title. 

How to create a new post, at least for now. Choose a command from the menu at the top of the screen. It opens up a new draft. When you make editing changes it saves as usual. We already have all this working in the first version, let's just port it across. 

#### 5/8/24; 9:38:29 AM by DW

Creating a new project outline and repo.

#### 5/3/24; 9:51:37 AM by DW

Let's create a new version of 1999.io where the posts are on WordPress, we don't render pages, but we do give them a Facebook-like user interface. 

