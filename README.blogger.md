### Blogger.com Installation

Installation requires eidting the HTML theme for you blog.

For installation, you need to edit your blog's theme. 
Goto <https://www.blogger.com/> once you are logged into you
blogs's Google account, you should see the administration page for your blog. 

To edit the theme, pick ***Theme*** from the list of the left side of the page.

It is a good idea to make a backup of your theme in case you want to go back to 
what you had before, there's a ***Backup / Restore*** button near the top right of 
the theme page, click it and follow the backup instructions (***DOwnload theme*** 
in the *Backup / Restore* dialog).

To edit the theme click the ***Edit HTML*** under the *Live on Blog* preview.

##### Step 1 - Add the macros (includables)

Add the following markup, in most of the provided themes you can 
add them right above the line that looks similar to:

    `<b:includable id='comment_picker' var='post'>`

it is easy to find if you click into the HTML editor and use `CTRL-F` 
or `CMD-F` then search for `id='comment_picker'`    

Copy and paste this code

    <b:includable id='twt_comments' var='post'>
      <b:if cond='data:numPosts == 1'>
        <b:if cond='data:post.isFirstPost'>
          <meta expr:content='data:post.title' name='twt-page-title'/>
          <meta expr:content='data:post.author' name='twt-author-name'/>
          <meta expr:content='data:post.timestampISO8601' id='twtPubDate' name='twt-published-at-ms'/>
          <meta expr:content='data:post.id' name='twt-article-id'/>
          <meta expr:content='data:post.url' name='twt-article-url'/>
          <div id='twt-comments'/>
        </b:if>
      </b:if>
    </b:includable>

    <b:includable id='twt_comment_count' var='post'>
      <div style="text-align: right;" class="post-header-line-1">
          <a expr:href='data:post.url+ "#twt-comments"' style="display: none;"><span twt-comment-count="" expr:twt-article-id='data:post.id'>0</span> comments</a>
      </div>
    </b:includable>

##### Step 2 - Add the comment section

Change (hint: try searching for `name='comment_picker'`):

    <b:include cond='data:blog.pageType in {&quot;static_page&quot;,&quot;item&quot;}' data='post' name='comment_picker'/>

to:

    <b:include cond='data:blog.pageType in {&quot;static_page&quot;,&quot;item&quot;,&quot;archive&quot;}' data='post' name='twt_comments'/>

##### Step 3 - Add comment counts

In two places usually (hint: search for `class='post-header'`), change:
          <div class='post-header'>
            <div class='post-header-line-1'/>
          </div>
to:
          <div class='post-header'>
            <b:include data='post' name='twt_comment_count'/>
          </div>

##### Step 4 - Include the script

Just before:

    </body>

insert this with your *World Table SiteId* where the zeros are: 

    <script twt-site-id="0000000000000000_0000000" src="https://app.worldtable.co/the-world-table.js"></script> 
  
If you don't have your *World Table SiteId*, visit this page:

   <https://app.worldtable.co/#!/sites>

you should see it near the bottom of the page.

##### Step 5 - Save your changes

Click the orange ***Save Theme*** button

##### Step 6 - Turn off built-in comments

Click the ***Settings*** item (below ***Theme***) on the left hand side of the admin page

Click ***Posts, comments and sharing settings*** under ***Settings***

For ***Comments Location*** choose ***Hide*** in the drop down menu.

##### Step 7 - Add the Top Comments List to the sidebar [optional]

Click the ***Layout*** item on the left hand side of the admin page.

Find the sidebar area, the spot called `sidebar-right-1` (or similar) is a great spot.

Click the ***Add a Gadget*** link in the sidebar section.

Click ***HTML/Javascript*** title or plus sign in the popup window

In the *Content* area type or paste this:

    <div id="twt-top-comments-list"></div>

It is usually best to leave the title empty

Adjust the position of the widget as desired.

Click ***Save***
