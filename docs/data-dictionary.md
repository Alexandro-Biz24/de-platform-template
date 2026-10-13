# Data dictionary

Types correspond to the raw types inferred by Pandas when reading the source CSV files. `object` represents string-like or mixed CSV values.

`Yes` includes direct identifiers, indirect identifiers, financial information, behavioural data and user-generated content.

| Table | Column | Source type | Meaning | Personal data |
|---|---|---|---|---|
| `buyer` | `buyer_id` | `object` | Unique buyer identifier | Yes — indirect identifier |
| `carrier` | `carrier_id` | `int64` | Unique carrier identifier | No |
| `carrier` | `carrier_name` | `object` | Carrier name | No |
| `cart` | `cart_id` | `object` | Unique shopping-cart identifier | Yes — indirect identifier |
| `cart` | `buyer_id` | `object` | Buyer owning the cart | Yes — indirect identifier |
| `cart` | `total_qty` | `object` | Total quantity in the cart | Yes — behavioural data |
| `cart` | `total_price` | `object` | Total value of the cart | Yes — financial behaviour |
| `cart_items` | `cart_id` | `object` | Shopping-cart identifier | Yes — indirect identifier |
| `cart_items` | `p_id` | `object` | Product identifier | No |
| `cart_items` | `qty` | `object` | Product quantity in the cart | No |
| `category` | `category_id` | `int64` | Unique product-category identifier | No |
| `category` | `name` | `object` | Category name | No |
| `category` | `c_desc` | `object` | Category description | No |
| `customer` | `c_id` | `object` | Unique customer identifier | Yes — indirect identifier |
| `customer` | `fname` | `object` | Customer first name | Yes — direct identifier |
| `customer` | `lname` | `object` | Customer last name | Yes — direct identifier |
| `customer` | `phone` | `int64` | Customer telephone number | Yes — direct identifier |
| `customer` | `email` | `object` | Customer email address | Yes — direct identifier |
| `customer` | `pwd` | `object` | Legacy customer password credential | Yes — highly sensitive |
| `customer_payment` | `payment_id` | `int64` | Customer payment-method identifier | Yes — financial identifier |
| `customer_payment` | `c_id` | `object` | Customer identifier | Yes — indirect identifier |
| `customer_payment` | `is_default` | `int64` | Indicates the default payment method | Yes — account preference |
| `customer_shipping` | `address_id` | `int64` | Customer shipping-address identifier | Yes — indirect identifier |
| `customer_shipping` | `c_id` | `object` | Customer identifier | Yes — indirect identifier |
| `customer_shipping` | `is_default` | `int64` | Indicates the default shipping address | Yes — account preference |
| `daily_deals` | `p_id` | `object` | Product receiving the deal | No |
| `daily_deals` | `deal_date` | `object` | Date on which the deal applies | No |
| `daily_deals` | `discount` | `object` | Discount applied by the deal | No |
| `discount` | `discount_id` | `object` | Unique discount identifier | No |
| `discount` | `discount_name` | `object` | Discount name | No |
| `discount` | `d_desc` | `object` | Discount description | No |
| `discount` | `discount_amt` | `object` | Discount amount or rate | No |
| `order_items` | `order_id` | `int64` | Order containing the item | Yes — transaction identifier |
| `order_items` | `p_id` | `object` | Purchased product identifier | No |
| `order_items` | `qty` | `int64` | Quantity purchased | No |
| `order_items` | `price_at_purchase` | `float64` | Unit price at the time of purchase | No |
| `orders` | `order_id` | `int64` | Unique order identifier | Yes — transaction identifier |
| `orders` | `buyer_id` | `object` | Buyer who placed the order | Yes — indirect identifier |
| `orders` | `discount_id` | `float64` | Discount applied to the order | No |
| `orders` | `payment_id` | `int64` | Payment method used for the order | Yes — financial identifier |
| `orders` | `order_date` | `object` | Date on which the order was placed | Yes — transaction metadata |
| `payment` | `transaction_id` | `int64` | Unique payment transaction identifier | Yes — financial identifier |
| `payment` | `order_id` | `int64` | Order associated with the payment | Yes — transaction identifier |
| `payment` | `payment_id` | `int64` | Payment-method identifier | Yes — financial identifier |
| `payment` | `amount` | `float64` | Amount paid | Yes — financial data |
| `payment` | `method` | `object` | Payment method used | Yes — financial data |
| `payment` | `status` | `object` | Payment status | Yes — transaction metadata |
| `payment` | `created_at` | `object` | Payment creation timestamp | Yes — transaction metadata |
| `payment_details` | `payment_id` | `int64` | Payment-method identifier | Yes — financial identifier |
| `payment_details` | `card_no` | `int64` | Payment card number | Yes — highly sensitive |
| `payment_details` | `cvv` | `int64` | Payment card verification value | Yes — highly sensitive |
| `payment_details` | `expiry_date` | `object` | Payment card expiry date | Yes — sensitive financial data |
| `payment_details` | `billing_address` | `object` | Cardholder billing address | Yes — direct identifier |
| `product` | `p_id` | `object` | Unique product identifier | No |
| `product` | `p_name` | `object` | Product name | No |
| `product` | `p_desc` | `object` | Product description | No |
| `product` | `price` | `float64` | Current product price | No |
| `product` | `qty` | `int64` | Available product quantity | No |
| `product` | `category_id` | `int64` | Product-category identifier | No |
| `product_images` | `p_id` | `object` | Product identifier | No |
| `product_images` | `p_image` | `object` | Product image location or value | No |
| `product_reviews` | `p_id` | `object` | Reviewed product identifier | No |
| `product_reviews` | `review_id` | `int64` | Review associated with the product | Yes — indirect identifier |
| `returns` | `return_id` | `object` | Unique return identifier | Yes — transaction identifier |
| `returns` | `buyer_id` | `object` | Buyer requesting the return | Yes — indirect identifier |
| `returns` | `p_id` | `object` | Returned product identifier | No |
| `returns` | `order_id` | `object` | Original order identifier | Yes — transaction identifier |
| `review` | `review_id` | `int64` | Unique review identifier | Yes — indirect identifier |
| `review` | `buyer_id` | `object` | Buyer who submitted the review | Yes — indirect identifier |
| `review` | `r_desc` | `object` | User-written review content | Yes — user-generated content |
| `review` | `title` | `object` | User-written review title | Yes — user-generated content |
| `review` | `rating` | `int64` | Rating submitted by the buyer | Yes — behavioural data |
| `review` | `seller_product_flag` | `object` | Indicates whether the review concerns a seller or product | No |
| `review_images` | `review_id` | `int64` | Review associated with the image | Yes — indirect identifier |
| `review_images` | `review_img` | `object` | Image attached to a review | Yes — potentially user-generated content |
| `seller` | `seller_id` | `object` | Unique seller identifier | Yes — if the seller is an individual |
| `seller` | `seller_type` | `object` | Seller classification | No |
| `seller` | `seller_name` | `float64` | Seller name | Yes — potentially direct identifier |
| `seller_products` | `seller_id` | `object` | Seller identifier | Yes — if the seller is an individual |
| `seller_products` | `p_id` | `object` | Product sold by the seller | No |
| `seller_reviews` | `seller_id` | `object` | Reviewed seller identifier | Yes — if the seller is an individual |
| `seller_reviews` | `review_id` | `int64` | Review associated with the seller | Yes — indirect identifier |
| `shipment` | `shipping_id` | `int64` | Unique shipment identifier | Yes — transaction identifier |
| `shipment` | `order_id` | `int64` | Order associated with the shipment | Yes — transaction identifier |
| `shipment` | `p_id` | `object` | Shipped product identifier | No |
| `shipment` | `carrier_id` | `int64` | Carrier responsible for delivery | No |
| `shipment` | `shipment_type` | `object` | Delivery service type | No |
| `shipment` | `status` | `object` | Current shipment status | Yes — transaction metadata |
| `shipment` | `est_delivery_date` | `object` | Estimated delivery date | Yes — transaction metadata |
| `shipment` | `actual_delivery_date` | `object` | Actual delivery date | Yes — transaction metadata |
| `shipping_details` | `address_id` | `int64` | Unique shipping-address identifier | Yes — indirect identifier |
| `shipping_details` | `street_address` | `object` | Street and building address | Yes — direct identifier |
| `shipping_details` | `city` | `object` | Shipping city | Yes — location data |
| `shipping_details` | `state` | `object` | Shipping state or region | Yes — location data |
| `shipping_details` | `zip` | `object` | Shipping postal code | Yes — location data |
| `shipping_details` | `country` | `object` | Shipping country | Yes — location data |
| `shipping_details` | `phone` | `int64` | Recipient telephone number | Yes — direct identifier |
| `subscription` | `subscription_id` | `int64` | Unique subscription identifier | Yes — indirect identifier |
| `subscription` | `c_id` | `object` | Subscribed customer identifier | Yes — indirect identifier |
| `subscription` | `start_date` | `object` | Subscription start date | Yes — account history |
| `subscription` | `end_date` | `object` | Subscription end date | Yes — account history |
| `wishlist_item` | `product_id` | `object` | Product saved in the wishlist | No |
| `wishlist_item` | `buyer_id` | `object` | Buyer owning the wishlist | Yes — indirect identifier |

## Critical findings

- `pwd`, `card_no` and `cvv` must be treated as highly sensitive and excluded from future analytical ingestion.
- Customer names, email addresses, telephone numbers and addresses require restricted access and auditing.
- `phone`, `card_no` and `cvv` were inferred as integers, which can remove leading zeros. This source-schema issue must be handled after Bronze.
- `seller_name` was inferred as `float64`, suggesting empty or inconsistent source values that must be investigated in Silver.
- Empty tables have unreliable inferred `object` types; their schemas must be revalidated when data first arrives.