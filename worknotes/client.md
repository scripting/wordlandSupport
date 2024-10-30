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

