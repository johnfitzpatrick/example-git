#Chef Fundamentals 3.0
##Part 1
###Lesson Objectives
- What is a resource
- Convergence
- Idempotency


###Narrative
Students log into a node containing ChefDK+Docker+Kitchen Docker

Use `chef-apply` on:-

    file 'hello.txt' do
      content 'Hello World'
      action :create
    end

Then
- Rerun chef-apply - no change
- Manually edit ‘hello.txt’
- Rerun chef-apply - fixed
- etc
- Delete the file:-


    file 'hello.txt' do
          action :delete
    end

`file` is one resource, but there are other resources:-
- `package ntpd`
- `service ntpd`

##Part 2
###Lesson Objectives
- Introduction to Test Driven Development
- Intro to Test Kitchen
- Intro to Serverspec
- Intro to Chefspec

###Narritive
Lesson has install apache them stand up a homepage

    $ chef generate cookbook apache
    $ vi kitchen.yml

- Change vagrant -> docker
- Comment out ubuntu


     kitchen list
     kitchen create
     kitchen converge
     kitchen login


Explain to class we want to have a web page. So have the class interactively write `serverspec` tests for
- package
- service
- file

Then

    kitchen destroy
    kitchen verify

__Fail__!  Now write the recipe.

Change `file` resource to `template` resource.


##Part 3
###Lesson Objectives
- Introduce `chef-client`
- Intro to node object & attributes

###Narrative

Run `chef-client -z /path/to/cookbooks`

Then show them `nodes/foo.json`.

Explain
- `ohai`
- `node[:platform]`

##Part 4
###Lesson Objectives
- Introduce Chef Server
- Introduce Workstation
- Introduce Roles and Environments
- Introduce search

###Narrative
- But wait - we want another node - do I have to copy my cookbook across? Introducing the chef server.
- But wait - we want a specific devel environment - so now we also need a Workstation.

We write more recipes that incude search, and __bootstrap__ (!!new concept!!) two nodes - Two options
- Option 1
 - We set up two roles - [web] and [loadbalancer].  LB searches for Webserver
 - We bootstrap two nodes - one [web], and one [web] & [lb]
 - lb listens on port 80, webserver on 8080
- Option 2
 - We have role [web] and role [nagios], and bootstrap those nodes

- We set the port as attributes in Role.

We introduce Environments and setting attributes in environments

##Part 4
###Lesson Objectives
- Introduce the Authentication model
- community cookbooks


###Narrative
- Have the kids write a 'delete validation' recipe form scratch
- Download the `chef-client` cookbook and compare against their own.
- Key learnings - no backup, not on server, etc etc
- Do we include the chef-client run, or too much for fundamentals?

##Part 5
###Lesson Objectives
- Intro to CI/CD pipeline

###Narrative
Demo only of using github and jenkins cookbook to deliver a full end to end CI pipeline



##Other Topics To Cover

These topics could/should be included in some way, either explicitly in a separate section, or implicitly as part of an existing lab.

- include_recipe
- cookbook dependencies
- databags
