rails_image
===========


```ruby
class PicsController < ApplicationController

	require "base64"

	def simple

		@pic = Base64.encode64(File.read(Rails.root.to_s + "/empty.png"))

	end

	def create

		imgup = params[:stuff].read                  	# the data
		#imgup = params[:stuff].original_filename		# its file name on the client
		#imgup = params[:stuff].content_type.chomp    	# something like "image/jpg" or "image/png"

		@pic = Base64.encode64(imgup)

		render :action => 'simple', :layout => false

	end

end
```


```html
<form method="post" action="create" enctype="multipart/form-data">

	<input type="file" name="stuff"><br>

	<input name="authenticity_token" type="hidden" value="<%= form_authenticity_token %>">

	<input type="submit"><br><br> 

	<img src="data:image/*;base64,<%= @pic %>" width=200>

</form>
```









