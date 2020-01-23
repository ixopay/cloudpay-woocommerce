# Disclaimer

**Warning!** This docker image is dedicated for demo usage, thus it is not recommended to use it in production.

But you can take the Dockerfile in this repository as an guideline on how to setup the PGC Gateway Integration Extentension in your freshly installed shop.
You can get in touch with support@ixolit.com to request access to the authenticated public demo version of this images and get an first impression by yourself.

---

You can Use this docker image in 2 diffrent ways:

1. [DEV] runs plugin setup with local source code:

```
sudo docker-compose up --build --force-recreate --renew-anon-volumes
```

2. [Github] execute setup & configuration script at runtime (with plugin from github):

```
# Update ENV Values inside `docker-compose.github.yml` to point `REPOSITORY` to an actual Repository
# If REPOSITORY has an invalid Value the Setup script wont run!
sudo docker-compose -f docker-compose.github.yml up --build --force-recreate --renew-anon-volumes
```