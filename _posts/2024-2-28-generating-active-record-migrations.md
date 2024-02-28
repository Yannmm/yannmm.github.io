---
layout: post
title: Generating Active Record Migrations
tags: rails
---

## Why

Migration in Rails is **a tool that allows the developer to use Ruby code to change an application's database schema**. Instead of using SQL scripts, we use Ruby code, which is database independent. Active Record will also update your **db/schema.rb** file to match the up-to-date structure of your database.

  

## What

Migrations are stored as files in the **db/migrate** directory. In each migration file defines a migration class, which prefixed by a timestamp of the current date and time.

Rails provide a tool for you to generate migration in command-line.  Usage:

```
bin/rails generate(g) migration MIGRATION_NAME [field[:type][:index] field[:type][:index]] [options]
```

Notice, fiels parameters decide what columns to add or remove.

  

## How

### Creating New Tables


MIGRATION_NAME is **create_{table_name}** followed by a list of column names and types.

```
rails generate migration CreateProducts name:string part_number:string
```

### Adding Columns

MIGRATION_NAME is `add_{column1}_{column2}_to_{table_name}` followed by a list of column names and types. Notice, column names should match.

```
rails g migration add_name_part_number_to_products name:string part_number:string
```

### Removing Columns

MIGRATION_NAME is **remove_{column1}_{column2}_to_{table_name}** followed by a list of column names and types. Types are optional but can be useful for reverting.

### Creating Standalone Migrations

You can create an empty migration, which defines an empty change method.

```
rails g migration {any_name_you_want}
```

### Model Generators

The model, resource, and scaffold generators will create migrations appropriate for adding a new model.

```
rails generate model Product name:string description:text
```
  

## Where

This is database-related operation. Please **distinguish** from model (ActiveRecord) behaviors.

  

## When

Each time before you want to change database schema, like adding new tables, changing or deleting existing tables.

  
  

## Who

- [Active Record Migrations](https://guides.rubyonrails.org/active_record_migrations.html#generating-migrations)

- [ActiveRecord::ConnectionAdapters::SchemaStatements - remove_column](https://api.rubyonrails.org/v7.1.2/classes/ActiveRecord/ConnectionAdapters/SchemaStatements.html#method-i-remove_column)

