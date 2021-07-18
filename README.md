# solr
docker run --name DockerSolr ^
-v DockerSolrShared/Danish:/opt/solr/server/solr/Danish ^
-v /Users/macbook/DockerSolrShared/English:/opt/solr/server/solr/English ^
-v /Users/macbook/DockerSolrShared/German:/opt/solr/server/solr/German ^
-d -p 1234:8983 -t solr

docker run --name DockerSolr -v /Users/macbook/DockerSolrShared/Danish:/opt/solr-8.6.1/server/solr/Danish -v /Users/macbook/DockerSolrShared/English:/opt/solr-8.6.1/server/solr/English -v /Users/macbook/DockerSolrShared/German:/opt/solr-8.6.1/server/solr/German -d -p 1234:8983 -t solr

opt/solr-8.6.1/server/solr-webapp/webapp/

docker run -—name DockerSolr -v /Users/macbook/solrver/server/solr/configsets/sample_techproducts_configs/conf:/opt/solr-8.6.1/server/solr/configsets/sample_techproducts_configs/conf exec -it -p 4321:8983 -t solr /bin/bash




You can SSH in to docker container as root by using
docker exec -it --user root <container_id> /bin/bash
Then change root password using this
passwd root
Make sure sudo is installed check by entering
sudo
if it is not installed install it
apt-get install sudo
If you want to give sudo permissions for user dev you can add user dev to sudo group
usermod -aG sudo dev
Now you'll be able to run sudo level commands from your dev user while inside the container or else you can switch to root inside the container by using the password you set earlier.
To test it login as user dev and list the contents of root directory which is normally only accessible to the root user.
sudo ls -la /root
Enter password for dev
If your user is in the proper group and you entered the password correctly, the command that you issued with sudo should run with root privileges.
root@7422633382ec:/var/solr/data/configsets/search_twitter/conf# rm -rf conf/
root@7422633382ec:/var/solr/data/configsets/search_twitter/conf# cp -r /opt/solr/server/solr/configsets/_default/conf/. .
root@7422633382ec:/var/solr/data/configsets/search_twitter/conf# ls -l
total 120
drwxr-xr-x 41 root root  1312 Aug 21 21:48 lang
-rw-r--r--  1 root root 55898 Aug 21 21:48 managed-schema
-rw-r--r--  1 root root   873 Aug 21 21:48 protwords.txt
-rw-r--r--  1 root root 49260 Aug 21 21:48 solrconfig.xml
-rw-r--r--  1 root root   781 Aug 21 21:48 stopwords.txt
-rw-r--r--  1 root root  1124 Aug 21 21:48 synonyms.txt
root@7422633382ec:/var/solr/data/configsets/search_twitter/conf# curl -X GET 'http://localhost:8983/solr/admin/cores?action=create&name=search_twitter&instanceDir=configsets/search_twitter'
{
  "responseHeader":{
    "status":0,
    "QTime":1623},
  "core":"search_twitter"}
root@7422633382ec:/var/solr/data/configsets/search_twitter/conf# curl -X GET 'http://localhost:8983/solr/search_twitter/schema/fields'
{


