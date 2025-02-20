# 🏗️ Installation

## Use Twake in SaaS

You can test or use Twake in our SaaS : [web.twake.app](https://web.twake.app)

## Run Twake in your server

### Install docker

If you don't have docker in your server, you have to install it.

```text
sudo apt-get update
sudo apt-get -y install apt-transport-https ca-certificates curl gnupg2 software-properties-common
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get -y install docker-ce --allow-unauthenticated
```

### Install docker-compose

Twake use docker-compose. If it is not installed in your server :

```text
sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

### Install and run Twake

You can install Twake on your server with this command

```text
git clone https://github.com/TwakeApp/Twake.git
cd Twake/twake
cp docker-compose.yml.dist docker-compose.yml
docker-compose up -d
```

> To run ElasticSearch \(optional, but enabled by default in the Twake docker-compose\) you must increase the max\_map\_count of your system: [https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html\#\_set\_vm\_max\_map\_count\_to\_at\_least\_262144](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html#_set_vm_max_map_count_to_at_least_262144)
>
> To fix an other bug with ElasticSearch container, you must also run this command: `chmod 777 ./docker-data/es_twake` \(create the folder if it doesn't exists in your docker-compose.yml folder\)

Twake will be running on port 8000 🎉

### Ship Twake in production

See how to [detach configuration](../configuration/). And then how to [update security keys](../configuration/security.md), and finally how to use your [custom domain](../configuration/custom-domain-and-https/).

### Update Twake

```text
docker-compose stop
docker-compose rm #Remove images (not volumes so your data is safe)
docker-compose pull #Get new images
docker-compose up -d
docker-compose exec nginx yarn build #If you have custom frontend configuration
```

## Requirements and scalability

Currently you'll need at least a **2 cpu + 4 gb of ram** machine for **20-50 users** depending on their usage and with ElasticSearch disabled.

If you enable ElasticSearch, use two machines, or limit the cpu/ram dedicated to it and use a larger machine \(at least 2gb of ram and 1 cpu dedicated to ES for 20-50 users\).

If you need to deploy Twake for more users, you can use only one big machine up to 500 users \(Will need something like **12 cpu and 32go of ram**\), then you'll need to use multiple nodes.

{% hint style="info" %}
We deployed Twake on production for companies of 10 to 50 users in a single node. We also deployed Twake in a scalable mode and we support currently thousands of concurrent users.

If you deploy Twake in your own company we would love to have your feedback here [https://github.com/TwakeApp/Twake/issues/289](https://github.com/TwakeApp/Twake/issues/289) to improve our requirements documentation.
{% endhint %}

Now if you want to scale with Twake and support thousand of users, click on the link below :

{% page-ref page="scale-with-twake.md" %}

