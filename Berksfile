branch = 'dev'

jira_git_url = 'git@github.com:/xianfengyuan'

jira_cookbooks = "
apt
ark
apache2
build-essential
chef-sugar
database
java
jira
jira-menlo
mariadb
mysql
mysql2_chef_gem
mysql_connector
openssl
postgresql
rbac
smf
yum
yum-epel
yum-mysql-community
".split

# Include Opsworks Cookbooks
opsworks_cb_path = '/opt/aws/opsworks/current/cookbooks'
opsworks_cookbooks = Dir[opsworks_cb_path + '/*'].select { |f| File.directory?(f) }.map { |f| File.basename(f) }

# Remove any opsworks cookbooks that we use
opsworks_cookbooks -= jira_cookbooks

# Get all of the opworks cookbooks
opsworks_cookbooks.each do |cb|
  cookbook(cb, path: File.join(opsworks_cb_path, cb))
end

# Get all custom cookbooks
jira_cookbooks.each do |thiscookbook|
  cookbook(thiscookbook, git: jira_git_url + '/chef_' + thiscookbook, branch: branch)
end
