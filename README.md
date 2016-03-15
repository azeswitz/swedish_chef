10.0.2.15  (vagrant ubuntu chef_learn)
2222 -> 22

ssh -i /Users/AZeswitz/Data/chef/learn_chef/.vagrant/machines/default/virtualbox -l vagrant -p 2222 localhost

knife bootstrap localhost --ssh-port 2222 --ssh-user vagrant --sudo --identity-file /Users/AZeswitz/Data/chef/learn_chef/.vagrant/machines/default/virtualbox --node-name node1 --run-list 'recipe[learn_chef_apache2]'

knife list
knife node show node1

Make changes to the cookbook
Update the chef server
knife cookbook upload learn_chef_apache2

Update the node
knife ssh ADDRESS 'sudo chef-client' --manual-list --ssh-user USER --identity-file IDENTITY_FILE
knife ssh localhost --ssh-port 2222 'sudo chef-client' --manual-list --ssh-user vagrant --identity-file /Users/AZeswitz/Data/chef/learn_chef/.vagrant/machines/default/virtualbox


##To clean up
knife node delete node1 --yes
knife client delete node1 --yes



##Change code in the cookbook
##Upload to Chef Server
knife cookbook upload learn_chef_apache2

##Run chef-client on server (using knife)
knife ssh localhost --ssh-port 2222 'sudo chef-client' --manual-list --ssh-user vagrant --identity-file /Users/AZeswitz/Data/chef/learn_chef/.vagrant/machines/default/virtualbox


Other useful commands
kitchen list
kitchen login
#generate a key for encrypted_data_bag_secret
openssl rand -base64 512 | tr -d '\r\n' > ~/learn-chef/.chef/encrypted_data_bag_secret
#Get the latest version of any recipe
knife cookbook site show apt | grep latest_version


#start project
#create the cookbook in the cookbooks directory
chef generate cookbook cookbooks/awesome_customers_ubuntu
#update the .kitchen.yaml file to describe the server specs
#https://learn.chef.io/manage-a-web-app/ubuntu/create-the-cookbook/
#downloads desired box and installs chef client
kitchen converge
#include apt
#modify firewall
#generate the firewall recipe
chef generate recipe cookbooks/awesome_customers_ubuntu firewall
#generate an attributes file for the purpose of storing data (eg port ranges for firewall rules)
chef generate attribute cookbooks/awesome_customers_ubuntu default
#add httpd - add dependency to metadata.rb
chef generate recipe cookbooks/awesome_customers_ubuntu web
#tweak to add attributes to abstract hardcoded values (default.rb)
kitchen converge
#generate key for encrypted_data_bag_secret
#create the databag password in [Cookbook]/data_bags/database_passwords/[filename].json
#encrypt the file
knife data bag from file database_passwords mysql_customers.json --secret-file .chef/encrypted_data_bag_secret --local-mode



openssl rand -base64 512 | tr -d '\r\n' > /Users/AZeswitz/Data/chef/learn_chef/.chef/encrypted_data_bag_secret
