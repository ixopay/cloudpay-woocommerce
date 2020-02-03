# Docker demo & development environment

**Warning!** This docker image is dedicated for development & demo usage, we don't recommended to use it in production.

---

## Usage

To quickly spawn a Woocommerce test shop with a plugin tagged at our github.com repository:

Clone our plugin repository and run the following command from the plugin root directory:

```
 REPOSITORY="https://github.com/ixopay/pgc-woocommerce" \
 BRANCH="master" \
 URL="http://localhost" \
 WORDPRESS_USERNAME=dev \
 WORDPRESS_PASSWORD=dev \
  docker-compose -f docker-compose.github.yml up --build --force-recreate --renew-anon-volumes
```

To develop and test plugin changes, you can run the following docker-compose command from the plugin root directory, to start a Woocommerce shop & initialize a database with a bind mounted version of the plugin. The shop will be accessible via: `http://localhost/wp-admin`.

```
 BITNAMI_IMAGE_VERSION=latest \
 URL="http://localhost" \
 WORDPRESS_USERNAME=dev \
 WORDPRESS_PASSWORD=dev \
  docker-compose up --build --force-recreate --renew-anon-volumes
```

Please note:

- By running the command we always run a complete `--build` for the shop container, `--force-recreate` to delete previous containers and always delete
the previous instance's storage volumes via `--renew-anon-volumes`. We don't support to change variables without rebuilding the full container.
- We currently use Bitnami Docker images as base for the environment and add our plugin.
- Further environment variables can be set, please take a look at `docker/Dockerfile` for a complete list.

### Customize Settings

Defaults for the Docker build are configured in the `.env` file. You can either:
-  set variables via environment variable or
- persist them in the `environment:` section of the respective docker-compose file.

### Platform credentials

To successfully test a payment flow you will need merchant credentials for the payment platform and set them via the following environment variables:

```bash
 # Base url for payment plaform API
 SHOP_PGC_URL="https://sandbox.paymentgateway.cloud"
 # Credentials for payment platform API
 SHOP_PGC_USER="test-user"
 SHOP_PGC_PASSWORD="test-pass"
 SHOP_PGC_API_KEY="key"
 SHOP_PGC_SECRET="secret"
 SHOP_PGC_INTEGRATION_KEY="int-key"
```

Additional platform specific settings:

```bash
 # Enable or disable payments for specific schemes
 SHOP_PGC_CC_AMEX="True"
 SHOP_PGC_CC_DINERS="True"
 SHOP_PGC_CC_DISCOVER="True"
 SHOP_PGC_CC_JCB="True"
 SHOP_PGC_CC_MAESTRO="True"
 SHOP_PGC_CC_MASTERCARD="True"
 SHOP_PGC_CC_UNIOPNPAY="True"
 SHOP_PGC_CC_VISA="True"

 # Either use "debit" or "preauthorize" transaction requests
 SHOP_PGC_CC_TYPE="debit"
 SHOP_PGC_CC_TYPE_AMEX="debit"
 SHOP_PGC_CC_TYPE_DINERS="debit"
 SHOP_PGC_CC_TYPE_DISCOVER="debit"
 SHOP_PGC_CC_TYPE_JCB="debit"
 SHOP_PGC_CC_TYPE_MAESTRO="debit"
 SHOP_PGC_CC_TYPE_MASTERCARD="debit"
 SHOP_PGC_CC_TYPE_UNIOPNPAY="debit"
 SHOP_PGC_CC_TYPE_VISA="debit"
```