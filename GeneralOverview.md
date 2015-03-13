# Overview #

The scope of the program is to provide a forum software that is flexible and able to provide for when news and wiki functionality is required within the forum software itself, in order to not disrupt the flow of information. However, there are a great deal of limitations to forum software which must also be addressed in order to modernize the programs and meet the expectations of today's internet user. In addition, in order to preserve individual communities while encouraging collaboration, a messaging system between installations will be established. Through this functionality, it will then be possible to not only bring together separate communities while still maintaining their individuality, it benefits the user by aggregating content they're interested in within a single community. Further, it more easily brings together users from other communities, giving more coverage, and making transitions easier, etc.

As for the implementation of these ideas, _INPHINET_ Cloud Commmunity Software is designed to provide a user interface akin to modern social networks, while integrating the redundant states and roles taken by other web software, including the blog, the wiki, and the forum. The software will allow the administrator to change the format in which information is displayed to the user using a drag & drop interface. In addition, it will allow the administrator to connect their software to other forum installations, allowing collections of messages to be shared beyond their origin.

Additional Features:
  * Each user will have a profile page which aggregates updates to topics which have been participated in, as well as private messages.
  * The software will keep track of a user's content, and will retain each message, even once it's been deleted from the public thread.
  * Preferences (users) and Settings (admins) can be edited either through a control panel, or in the context of the element, much like a widget. (denoted by an editing symbol, on hover, most likely a stylized "i")

# Design Outline #

## Message Modes ##
  * Talk (Blue) - Equivalent: forums and lists
  * Wiki (Green) - Equivalent: Wiki pages & discussion
  * News (Yellow) Equivalent: Blog posts & comments

## Overall Layout ##
  * Categories
    * Topics
      * Messages
        * Comments

## Categories ##
Similar to individual forums within a forum software.

## Topics ##
Synonymous with threads.

It's important to mark not only which topics the user has read, but also which ones they've participated in. Also, it's a good idea to mark the place in the topic with the last message available when they had last read that topic.

## Messages ##
Synonymous with posts. What is contained in a message:
  * Message Body
  * Participants - Users who have edited
  * Body History
  * Breadcrumbs - From where did the message originate, and which topics it's being displayed within.
  * Permissions

Only the User's profile icon is displayed next to a message. Further information is expanded into the space next to the message depending on which icon is hovered over.

## Comments ##
Initially it was planned to introduce a single-level indentation comment system per-message. It may probably better to go the traditional route, and allow comments to reference the text from other messages in-line with the message body. However, ratings, or 'likes', are a great idea, and should be implemented at once. This is because it acknowledges the quality of the contribution, and this helps reinforce good posts throughout the community. Negative ratings, or 'dislikes', should probably be avoided, however, or available as a preference.

## Users ##
Registration is done through the software, and not using OpenID or Google Accounts. This is because of the complex and proprietary user system being employed. Fortunately, to post to other sites using _INPHINET_, if two communities are connected, it will be a simple matter to post to the other, on their community, or in categories or topics inside the origin community.

If two communities aren't connected by administration, perhaps there could be guest posters, I'll have to think on that. Regardless, there will need to be a facility for reconciling two users with the same email address.

Email address is how the user will be tracked within the system, and how they will login. Display names can be changed at will, but there will be a name history in their profile. If there are two users with the same nickname, hilarity ensues, but the software should not have a problem. Okay, fine, there might need to be some checking on that, as well.

When communities are connected, users from one community can post to the other community. Their profile information is updated on their origin server, in addition to their messages, which are also stored on the origin server. Their profile will display their relationship with the other community, and how many messages they've made over there.

## Profile ##
It's important to display information relevant prominently to the user once they return to the site. Updates will be marked read once displayed, though, they can be Starred, which will continue starring updates from that thread or user. Updates can be retrieved as far back as they go.
  * General Updates (Topics which have been posted to since your last visit, and how many messages have been posted since)
  * Private Messages
  * Comments & Ratings to your posts

Fine-grained user statistics will also be kept track of and displayed in their profile, because they're fun. They will include: post count, thread count, replies to thread, join date, and account origin.

## Posting ##
A simple markup interface will be provided, with buttons to add markup to the document, much like Wikipedia. Standard BBCode will be used, and URLs will not have quotes around them in the url tag, like phpBB.

Saving drafts while writing a post or comment is a very good idea, to reduce frustration and information loss. Further, a user's post will be saved like a document, and kept within the program, forever, even if it's removed from public view. Contributors will also have copies, adn these will be shared. Posts and comments will be displayed separate from each other.

# Technical Considerations #

## XMPP ##
The XMPP is used for inter-server communication to instantly let the other server know that there is a new post available, and how to get it.
One possibility is to use XMPP to only give information as to how to get the post information from the server (such as or similar to a URL), and also, the forum software version, in order to minimize traffic on XMPP, which has a daily limit of receiving 4GB and a maximum rate of 22 mb/minute. Fortunately, these are very generous limits.

XMPP could also be used to notify the software of an update hardcoded into the program to download from the central server, and possibly auto-update, depending upon the limitations of App Engine.

However, App Engine does provide a versioning feature, which is very convenient for the administrator.