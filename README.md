# Snippets For Auth/HTML in Rails

This repository consists of only an atom snippets file intended for writing authorization code and html forms using Rails syntax.

**A Few Notes:**

1. This ReadMe will show you how to use every snippet that is provided in this file. You have to clone this and copy it into your own snippet file anyways, so you can obviously pick and choose the snippets you need.

2. We know that there is a very fine line between creating useful snippets that will cut down busy work and creating snippets that would be construed as cheating. This is part of the reason why we're making this public. If you feel that any of the snippets defined here would be grounds for cheating (that means you, App Academy TAs), please post an issue on the github repository or on Slack, and we will take the necessary action that is required.

3. We tried to think of every snippet that would prove to be useful for us in an assessment scenario. As we got closer to the end, our brains got fried making the actual snippets which might have affected our cognitive abilities. If you feel that we might have missed a snippet that would be useful, please contribute to the repository. **This is your chance to be a part of project on github with multiple contributors, which is basically your future work life in a nutshell.** Clone the repository, create a branch, add your snippets, make the respective changes to the ReadMe, merge the branch to master, and then make a pull request and either Bilal or myself will merge your changes with the Master branch. We don't want to make everyone contributors because that might make things a bit messy, but I am willing to reconsider that.

4. Inconsistencies and poor naming convetions and prefixes will be fixed. Just notify of any problems you see.

## Snippets On File

### HTML Snippets

---

**View Form**

**prefix:** 'vf'

Creates a form tag where you can tab into the action and the method attributes. The created form tag follows rails view form syntax including the convention for the **name** attribute as a hash with a parameter.

**Tab Order**

  1. Tab into the action attribute to place the url. Default: "model_url"

  2. Tab into the method attribute to place the method. Default: "get"

**Use Example**
```html
<form action="<%= model_url %>" method="get">
</form>
```

---

**Submit Tag**

**prefix:** 'vfs'

Creates the input tag with the type "submit".

**Tab Order**

  1. Tab into the value attribute to replace the second word of the string for the submit button. Default: "Model!"

**Use Example**
```html
<input type="submit" value="Create Model!">
```

---

**Input Text**

**prefix:** 'it'

Creates the input tag with type "text" along with it's corresponding label.

**Tab Order**

  1. Tab into the for attribute of the label tag, and the id attribute of the input tag simultaneously and enter the corresponding input id. Default: "input_id"

  2. Tab into the label text field and enter the label name. Default: "label_name"

  3. Tab into the name attribute of the input tag, and the model_name text simultaneously in erb within the value attribute of the same tag, and enter the model name. Default: "model_name"

  4. Within the name attribute, table into the square brackets and enter the attribute. Default: "param_name".

  5. Tab into the value attribute and enter the model name within the erb injection. Default: "model_name".

  6. Tab into the place after the dot and enter the value attribute. Default: "attr_name".

**Use Example**
```html
<label for="input_id">label_name</label>
<input type="text" name="model_name[param_name]" value="<%= @model_name.attr_name %>" id="input_id">
```
---

**CSRF Injection**

**prefix:** 'csrf'

Creates the csrf_token ruby injection tag, which you define in the ApplicationHelper class using the 'csrf' prefix in ruby. The prefix is identical between html and ruby, but have different actions.

**P.S. YES, THIS IS THAT "AUTH THING" YOU PUT AT THE START OF FORMS.**

**Use Example**
```html
<%= csrf_token %>
```

---

**Input Password**

**prefix:** 'ip'

Creates the input tag with the type "password" along with its corresponding label. Tab into the label and the input attributes.

**Tab Order**

1. Tab into the for attribute of the label tag, and the id attribute of the input tag simultaneously and enter the corresponding name of the password. Default: "password"

2. Tab into the label text field and enter the label name. Default: "Password:"

3. Tab into the name attribute of the input tag, and enter the model name, typically **user** in the case of a password. Default: "user"

4. Within the name attribute, tab into the square brackets and enter the attribute. Default: "password".

**Use Example**
```html
<label for="password">Password:</label>
<input type="password" name="user[password]" id="password">
```

---

**Input Radio**

**prefix:** 'ir'

Creates the input tag with the type "radio" along with its corresponding label. Tab into the input attributes and then into the label attributes.

**Tab Order**

1. Tab into the name attribute, and the erb check of the input tag simultaneously and enter the corresponding name of the model. Default: "model_name"

2. Tab into the param_name in the name attribute and the erb check. Default: "param_name"

3. Tab into the value intended for the radio button in the value attribute and the erb check.

4. Tab into the id attribute of the input tag, and the for attribute of the label tag simultaneously, and enter any chosen id that they may correspond. Default: "value"

5. Tab into the label name of the label tag. This is another chosen value, but in this case for the user's experience. Use this to show a name next to a radio button. Default: "label_name"

**Use Example**
```html
<input
  type="radio"  
  name="model_name[param_name]"
  value="value"
  id="input_id"
  <%= model_name.param_name == "value" ? "checked" : "" %>>
<label for="input_id">label_name</label>
```

---

**Input Dropdown**

**prefix:** 'drp'

Creates the input tag with the type "dropdown" along with its corresponding label. Tab into the input attributes and then into the label attributes.

The same thing as the text input and the password input, but is more special. It enters the model_name, param_name, and value inside the params.

**Tab Order**

1. Tab into the for attribute of the label tag, and the id attribute of the select tag simultaneously, and enter any chosen id that they may correspond. Default: "input_id"

2. Tab into the label name. Default: "LabelName"

3. Tab into the name attribute of the select tag and enter the respective model name. Default: "model_name"

4. Tab into the brackets after the model name within the name attribute of the select tag. Default: "param_name"

**Use Example**
```html
<label for="input_id">LabelName</label>
<select
  name="model_name[param_name]"
  id="input_id">
</select>
```
---

## Ruby Snippets

List of all ruby snippets, what they do, and how to use them.

---

**CSRF Function**

**prefix:** 'csrf'

This snippet automatically creates a function that can be used through an HTML injection.

  The generated function should be placed in the ApplicationHelper of your Rails Project.

  After putting the function in Application helper, you can use the HTML snippet **CSRF Injection** by the prefix 'csrf' in an HTML form, directly after opening a form tag.

  You will need this html within your forms unless you prefer to have errors in your Rails app.

  **Use Example**
```ruby
def csrf_token
  "<input type='hidden' name='authenticity_token' value='#{form_authenticity_token}'>".html_safe
end
```

---

**Password Digest**

**prefix:** 'digest'

This snippet automatically stores a password digest from the current class as an encrypted password passed as an argument.

  This code is typically used in the ApplicationController of your Rails Project.

  **Tab Order**
  1. Allow renaming of the password\_digest.
  Default: "password_digest"

**Use Example**
  ```ruby
    self.password_digest = BCrypt::Password.create(password)
  ```

---

**Password Comparison**

**prefix:** 'cpwd'

This snippet automatically compares a password_digest to a password passed as an argument.

This code is typically used in the ApplicationController of your Rails Project.

**Use Example**
```ruby
  BCrypt::Password.new(self.password_digest).is_password?(password)
```

---

**Flash.now Error**

  **prefix:** 'fne'

  This snippet inserts code to store an error in Flash.now based on a given model name.

  **Tab Order**
  1. Changes name of the model of which to store the full message.
  Default: "model_name"

**Use Example**
  ```ruby
    flash.now[:errors] =  @model_name.errors.full_message
  ```

---

**Flash Error**

  **prefix:** 'fe'

  This snippet inserts code to store an error in Flash based on a given model name.

  **Tab Order**
  1. Changes name of the model of which to store the full message.
  Default: "model_name"

---

**Flash Generic**

  **prefix:** 'fg'

  This snippet inserts code to store any message in Flash based on a given model name.

  **Tab Order**
  1. Changes parameter of the flash in which to store the flash_type.
  Default: "param_name"

  2. Changes the name of the model that we want to retrieve the message from.
  Default "model_name"

  3. Changes the flash type or message to store in the flash.
  Default: flash_type

---

**Flash.now Generic**

  **prefix:** 'fng'

  This snippet inserts code to store any message in Flash.now based on a given model name.

  **Tab Order**
  1. Changes parameter of the flash in which to store the flash_type.
  Default: "param_name"

  2. Changes the name of the model that we want to retrieve the message from.
  Default "model_name"

  3. Changes the flash type or message to store in the flash.
  Default: flash_type

---

**Controller Actions: new, create, index, show, edit, update, destroy**

  **prefixes:** 'cn', 'cc', 'ci', 'cs', 'ce', 'cu', 'cd'

  Each of these seven snippets insert code for the corresponding controller action.
  These methods WILL require fine-tuning to work exactly as needed.

  **Tab Order**
  1. Changes the ivar name, as well the redirect url and param names.
  Default: "myNAME"

  2. Changes the class name.
  Default: "myCLASS"

  3. Exits the method.
  Default: N/A

---

**Controller Parameters**

  **prefix:** 'cp'

  Inserts the controller's strong parameter method.

  **Tab Order**
  1. Changes the param name.
  Default: "myNAME"

  2. Tabs to the permit parameters.
  Default: N/A

  3. Exits the method.
  Default: N/A
