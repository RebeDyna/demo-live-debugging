# Dynatrace Live Debugger End to End Demo Environment

--8<-- "snippets/disclaimer.md"
--8<-- "snippets/view-code.md"

The Demo environment will showcase the following:

- Setup of the **Dynatrace OneAgent** within a local Kuberentes cluster
- Debugging an application issue with **Dynatrace Live Debugger**
- Fixing a bug, rebuilding and deploying the fix to the cluster using Skaffold
- Validating the fix directly within the VSCode IDE using **Dynatrace Code Monitoring** extension

## Architecture

This demo uses the **Online Boutique** which is composed of 11 microservices written in different
languages that talk to each other over gRPC. It's setup to run inside a Kind Kubernetes cluster


| Service                                              | Language      | Description                                                                                                                       |
| ---------------------------------------------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| [frontend](/src/frontend)                           | Go            | Exposes an HTTP server to serve the website. Does not require signup/login and generates session IDs for all users automatically. |
| [cartservice](/src/cartservice)                     | C#            | Stores the items in the user's shopping cart in Redis and retrieves it.                                                           |
| [productcatalogservice](/src/productcatalogservice) | Go            | Provides the list of products from a JSON file and ability to search products and get individual products.                        |
| [currencyservice](/src/currencyservice)             | Node.js       | Converts one money amount to another currency. Uses real values fetched from European Central Bank. It's the highest QPS service. |
| [paymentservice](/src/paymentservice)               | Node.js       | Charges the given credit card info (mock) with the given amount and returns a transaction ID.                                     |
| [shippingservice](/src/shippingservice)             | Go            | Gives shipping cost estimates based on the shopping cart. Ships items to the given address (mock)                                 |
| [emailservice](/src/emailservice)                   | Python        | Sends users an order confirmation email (mock).                                                                                   |
| [checkoutservice](/src/checkoutservice)             | Go            | Retrieves user cart, prepares order and orchestrates the payment, shipping and the email notification.                            |
| [recommendationservice](/src/recommendationservice) | Python        | Recommends other products based on what's given in the cart.                                                                      |
| [adservice](/src/adservice)                         | Java          | Provides text ads based on given context words.                                                                                   |
| [loadgenerator](/src/loadgenerator)                 | Python/Locust | Continuously sends requests imitating realistic user shopping flows to the frontend.                                              |

<div class="grid cards" markdown>
- [Click Here to Begin :octicons-arrow-right-24:](getting-started.md)
</div>