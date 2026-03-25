# 🚀 UniDelivery -- Configuration & Setup Guide

## 📦 1. Clone the Microservices Repositories

Before running the project, clone all required services:

Base URL: https://github.com/orgs/UniDelivery-org/

### Clone each service:

``` bash
git clone https://github.com/UniDelivery-org/gateway.git
git clone https://github.com/UniDelivery-org/user-service.git
git clone https://github.com/UniDelivery-org/delivery-service.git
git clone https://github.com/UniDelivery-org/vehicle-service.git
git clone https://github.com/UniDelivery-org/identityDocs-service.git
git clone https://github.com/UniDelivery-org/wallet-service.git
git clone https://github.com/UniDelivery-org/transaction-service.git
git clone https://github.com/UniDelivery-org/trakingLog-service.git
```

⚠️ Make sure all folders are in the same root directory.

------------------------------------------------------------------------

## 🐳 2. Docker Compose Configuration

Create a `docker-compose.yml` file:

``` yaml
services:
  gateway:
    build: ./gateway
    container_name: gateway
    ports:
      - "8080:8080"

  user-service:
    build: ./user-service
    container_name: user-service
    ports:
      - "18081:8081"

  delivery-service:
    build: ./delivery-service
    container_name: delivery-service
    ports:
      - "18082:8082"

  vehicle-service:
    build: ./vehicle-service
    container_name: vehicle-service
    ports:
      - "18083:8083"

  identitydocs-service:
    build: ./identityDocs-service
    container_name: identityDocs-service
    ports:
      - "18084:8084"

  wallet-service:
    build: ./wallet-service
    container_name: wallet-service
    ports:
      - "18086:8086"

  transaction-service:
    build: ./transaction-service
    container_name: transaction-service
    ports:
      - "18087:8087"

  trackinglog-service:
    build: ./trakingLog-service
    container_name: trackinglog-service
    ports:
      - "18088:8088"
```

------------------------------------------------------------------------

## ▶️ 3. Run the Project

``` bash
docker-compose up --build
```

------------------------------------------------------------------------

## 💳 4. Stripe Webhook (Local Development)

To handle Stripe events locally, run the Stripe CLI inside Docker:

``` bash
docker run -it stripe/stripe-cli   --api-key your_stripe_api_key   listen   --forward-to http://host.docker.internal:8087/api/v1/transactions/stripe/webhook
```

🔑 Replace `your_stripe_api_key` with your actual Stripe secret key.

💡 This command forwards Stripe webhook events to your
`transaction-service`.

------------------------------------------------------------------------

## 🌐 5. Access Services

-   API Gateway → http://localhost:8080
-   User Service → http://localhost:18081
-   Delivery Service → http://localhost:18082
-   Vehicle Service → http://localhost:18083
-   Identity Docs → http://localhost:18084
-   Wallet Service → http://localhost:18086
-   Transaction Service → http://localhost:18087
-   Tracking Log Service → http://localhost:18088

------------------------------------------------------------------------

# 🎨 6. Frontend Setup (Angular)

## Clone Frontend

``` bash
git clone https://github.com/your-repo/frontend.git
cd frontend
```

## Install Dependencies

``` bash
npm install
```

## Run App

``` bash
npm start
```

App runs on: http://localhost:4200/

------------------------------------------------------------------------

# 🔑 7. Environment Config

Create:

src/environments/environment.ts

``` ts
export const environment = {
  production: false,
  apiUrl: 'http://localhost:8080/api',
  apiVersion: 'v1',
  stripePublicKey:
    'pk_test_your_key_here',
};
```

------------------------------------------------------------------------

# ⚙️ Frontend Tech Stack

-   Angular 20+
-   NgRx
-   TailwindCSS
-   Stripe
-   Leaflet Maps

------------------------------------------------------------------------

# 📁 Frontend Architecture

    src/app/
    ├── core/
    ├── features/
    ├── layouts/
    └── shared/

------------------------------------------------------------------------

## 🧪 8. Useful Commands

Stop:

``` bash
docker-compose down
```

Logs:

``` bash
docker-compose logs -f
```

Rebuild:

``` bash
docker-compose up --build
```

------------------------------------------------------------------------

## ⚠️ Notes

-   Install Docker & Docker Compose
-   Ensure ports are free
-   Each service must include a Dockerfile
