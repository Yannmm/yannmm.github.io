---
layout: post
title: Rails Learning Todos
tags: rails ruby
---

## 1. Add Column / Index / Foreign Key / References to Table

- `add_column(table_name, column_name, type, **options)`: Adds a new column of specified type.

- `add_foreign_key(from_table, to_table, **options)`: Adds a foreign key constraint to one or more columns, which should be added first.

- `add_index(table_name, column_name, **options)`:  Adds an index to one or more columns, which should be added first.

- `add_reference(table_name, ref_name, **options)`: Adds a references. It will: add a new column; add a foreign key constraint to that column; add index to that column with `unique: false`.

**Refs**
-  [ActiveRecord::ConnectionAdapters::SchemaStatements (rubyonrails.org)](https://api.rubyonrails.org/v7.1.2/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html)

## 2. Routing: Namespace vs Scope

- `namespace(path, options = {}, &block)` will
	1. prefix Uri and path with namespace; 
	2. require the module containing the controller; 
	3. expect the controller file locate at the namespace subfolder in the `controller` folder.

- `scope(*args)` support more detail control over
	1. Uri prefix 
	2. path prefix
	3. module of the controller and controller location.



**Refs**
- [Rails 5 Routes: Scope vs Namespace - Devblast](https://devblast.com/b/rails-5-routes-scope-vs-namespace)
- [Scoping Doc](https://api.rubyonrails.org/v7.1.2/classes/ActionDispatch/Routing/Mapper/Scoping.html) 


## 3. How respond_to works?

The mime-type-specific methods like html, xml are dynamically generated on the fly, using Ruby's `method_missing` method.


**Refs**

- [Rails 5 Routes: Scope vs Namespace - Devblast](https://devblast.com/b/rails-5-routes-scope-vs-namespace)
- [ActionController::MimeResponds (rubyonrails.org)](https://api.rubyonrails.org/v7.1.2/classes/ActionController/MimeResponds.html#method-i-respond_to)


## 4. Active Record Query Interface

`where` method allows you to specifiy conditions to limit the records returned, as the `WHERE`-part of the SQL statement.

For `where(*args)`, when the argument is an array, the first element should be the condition string and any additional arguments will replace `?` in it.

```
Book.where("title = ? AND out_of_print = ?", params[:title], false)
```

This is to prevent **SQL injection**.

**Refs**

- [Active Record Query Interface — Ruby on Rails Guides](https://guides.rubyonrails.org/active_record_querying.html#retrieving-multiple-objects-in-batches)


## 5. Range

A Range object represents a collection of values that are between given begin and end values.

Range can be constructed by `..`(include end value), `...`(exclude end value) or `Range.new`.


Any class implementing instance method `<=>` can be used to construct a range.

A range can be iterated over only if its elements implement instance method `succ`.

**Refs**

- [class Range - Documentation for Ruby 3.4 (ruby-lang.org)](https://docs.ruby-lang.org/en/master/Range.html)

- [class Object - Documentation for Ruby 3.4 (ruby-lang.org)](https://docs.ruby-lang.org/en/master/Object.html#method-i-3C-3D-3E)
