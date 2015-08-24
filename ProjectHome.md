Normally, to upload file,we will write some codes in the view page
like:

<% form\_for(:photo, :url => {:action => :create}, :html =>
{ :multipart => true}) do |form| -%>
> <p>
<blockquote>

<label for="">

Upload A Image:<br>
<br>
</label><br>
<br>
<br>
<%= form.file_field :uploaded_data %><br>
<%= submit_tag 'Upload' %><br>
</blockquote><blockquote></p>
<% end -%></blockquote>


Now,I coded some line of js, append to public/javascript/
application.js
now we just need to change little things as:
change: form\_for => remote\_form\_for
add: :ajaxupload => true


Then we got:


<% remote\_form\_for(:photo, :url => {:action => :create}) do |form| -%>
> <p>
<blockquote>

<label for="">

Upload A Image:<br>
<br>
</label><br>
<br>
<br>
<%= form.file_field :uploaded_data %><br>
<%= submit_tag 'Upload' %><br>
</blockquote><blockquote></p>
<% end -%></blockquote>


Now, file upload will post via a iframe without refresh the page.


But how about the rjs?
We won't forget it.
Add some codes in the controller as bellow:


  1. iframe request
> if params[:HTTP\_X\_REQUESTED\_WITH] && request.post?
> > render :template => 'photos/create.rjs', :layout =>
false, :content\_type => 'text/html'

> else
  1. normal request
> > respond\_to do |format|
> > > format.html {redirect\_to :action => 'new', :id => @photo if
request.post?}
> > > format.js

> > end

> end


Now we can render different views by the request type automatically.


The js code could down from:
http://railsajaxupload.googlecode.com/files/application.js

and a complete photo upload rails demo project:
http://railsajaxupload.googlecode.com/files/photo_upload.rar
use attachment\_fu plugin (require RMagick) and sqlite3 db engline


Tested with IE6,FireFox2.0,Safari3  on windows XPsp2.


some helpful links:


attachment\_fu tutorial:
http://clarkware.com/cgi/blosxom/2007/02/24#FileUploadFu


RMagick for windows:
http://rubyforge.org/frs/download.php/15132/RMagick-1.14.1_IM-6.3.0-7...


sqlite3 lib for windows:
http://www.sqlite.org/sqlite-3_4_0.zip
http://www.sqlite.org/sqlitedll-3_4_0.zip

