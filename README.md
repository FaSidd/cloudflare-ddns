# Cloudflare DDNS Setup 

Running [cloudflare ddns client](https://github.com/oznu/docker-cloudflare-ddns) container to update public IP of server

## Steps

Before running the container you will need to get an API key from your Cloudflare account

### Create Cloudflare API Key

Login in to your Cloudflare account.

Go to the top right after logging in and select the little guy and choose `my profile`.

Click the API Tokens tab and then click `Create Custom Token`.

Enter a token name and setup the `Permissions` section as follows:

![permissions-image](https://github.com/FaSidd/cloudflare-ddns/blob/main/images/permissions.png)

Then setup the `Zone Resources` section as follows:

![resources-image](https://github.com/FaSidd/cloudflare-ddns/blob/main/images/account.png)
  
In the last select box where it says `Select...` in the `Zone Rescources` you will select
your cloudflare account.

Then select `Continue to summary` at the bottom and confirm changes.

### Edit `docker-compose.yml` File

You should then be given an API key, copy that and add it to the `docker-compose.yml` file.
Also add your domain that you have setup with Cloudflare and put the subdomain you want to
connect for DDNS.

```yml
...
    environment:
      - API_KEY=YOUR-API-KEY
      - ZONE=example.com # root domain i.e. example.com
      - SUBDOMAIN=subdomain # ddns subdomain without the root
      - PROXIED=false
...
```

### Run the Container

After putting the info in the `docker-compose.yml` file now the container can be run.

```bash
docker-compose up -d
```

Now the container should be up and running.
