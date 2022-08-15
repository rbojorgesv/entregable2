# Entregable2

# Ecommerce_sv

1. Link dbdiafram
    https://dbdiagram.io/d/62f9738cc2d9cf52faa5728e

2.  Script Postgres

CREATE TABLE "users" (
  "id" serial PRIMARY KEY,
  "name" varchar NOT NULL,
  "email" varchar UNIQUE NOT NULL,
  "password" varchar NOT NULL,
  "country" varchar NOT NULL,
  "phone" varchar UNIQUE NOT NULL,
  "created_at" timestamp DEFAULT 'now()',
  "updated_at" timestamp DEFAULT 'now()'
);

CREATE TABLE "products" (
  "id" serial PRIMARY KEY,
  "product" varchar NOT NULL,
  "price" money NOT NULL,
  "item" int NOT NULL,
  "created_at" timestamp DEFAULT 'now()',
  "updated_at" timestamp DEFAULT 'now()'
);

CREATE TABLE "orders" (
  "id" serial PRIMARY KEY,
  "user_id" int,
  "address_id" int,
  "payment_method_id" int,
  "total_order" money,
  "created_at" timestamp DEFAULT 'now()',
  "updated_at" timestamp DEFAULT 'now()'
);

CREATE TABLE "order_details" (
  "id" serial PRIMARY KEY,
  "order_id" int,
  "product_id" int,
  "quantity" int NOT NULL,
  "price" money NOT NULL,
  "created_at" timestamp DEFAULT 'now()',
  "updated_at" timestamp DEFAULT 'now()'
);

CREATE TABLE "address" (
  "id" serial PRIMARY KEY,
  "user_id" int,
  "street" varchar NOT NULL,
  "city" varchar NOT NULL,
  "created_at" timestamp DEFAULT 'now()',
  "updated_at" timestamp DEFAULT 'now()'
);

CREATE TABLE "cart" (
  "id" serial PRIMARY KEY,
  "user_id" int,
  "product_id" int,
  "quantity" int NOT NULL,
  "created_at" timestamp DEFAULT 'now()',
  "updated_at" timestamp DEFAULT 'now()'
);

CREATE TABLE "payments" (
  "id" serial PRIMARY KEY,
  "payment_method" varchar NOT NULL,
  "created_at" timestamp DEFAULT 'now()',
  "updated_at" timestamp DEFAULT 'now()'
);

ALTER TABLE "orders" ADD FOREIGN KEY ("user_id") REFERENCES "users" ("id");

ALTER TABLE "orders" ADD FOREIGN KEY ("address_id") REFERENCES "address" ("id");

ALTER TABLE "cart" ADD FOREIGN KEY ("user_id") REFERENCES "users" ("id");

ALTER TABLE "cart" ADD FOREIGN KEY ("product_id") REFERENCES "products" ("id");

ALTER TABLE "address" ADD FOREIGN KEY ("user_id") REFERENCES "users" ("id");

ALTER TABLE "orders" ADD FOREIGN KEY ("payment_method_id") REFERENCES "payments" ("id");

ALTER TABLE "order_details" ADD FOREIGN KEY ("product_id") REFERENCES "products" ("id");

ALTER TABLE "order_details" ADD FOREIGN KEY ("order_id") REFERENCES "orders" ("id");


