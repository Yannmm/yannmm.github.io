---

layout: post

title: Active Record Encryption

tags: rails ruby

---

  

Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository (shown below).

  

![_config.yml]({{ site.baseurl }}/images/config.png)

  

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.

  

### Why

  
  

### What

  
  
  

### How

  1. Run `bin/rails db:encryption:init` from command-line to generate a random key set and copy them.

```
$ bin/rails db:encryption:init
Add this entry to the credentials of the target environment:

active_record_encryption:
  primary_key: EGY8WhulUOXixybod7ZWwMIL68R9o5kC
  deterministic_key: aPA5XyALhf75NNnMzaspW7akTfZp0lPY
  key_derivation_salt: xEY0dt6TZcAMg52K7O84wYzkjvbA62Hz

```

2. Run `VISUAL="code --wait" bin/rails credentials:edit` from command-line. In the opened editor, pasted above content to `credentials.yml.enc`. Be noticed, this file should be in editable state.

3. Close above file panel, now you should be good to go.
  

### Where

  
  

### When

  
  
  

### Who