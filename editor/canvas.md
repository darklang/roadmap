# Canvas

## \#\# Dark v1

Dark v1 had a number of problems 

### Infrastructure view

The Dark infrastructure view is intended as a better way to view your compoents of your infratructure than files and folders. Instead, you view your infrastructure according to it's structure - that is, the same way you would see it if a senior engineer was drawing your infrastructure on the whiteboard.

An example:

![](../.gitbook/assets/messages-image-2551186841-.jpeg)

This is a simple app that probably does something like project tracking, and it has 3 services: users, templates, and projects. Each of the HTTP routes is clustered around the database that they affect. Some of the DBs and routes have stats showing. The lines between the different routes represent traffic. 

