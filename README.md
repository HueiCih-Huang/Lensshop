# Lensshop
erDiagram
    USERS ||--|| CARTS : "Owns (1:1)"
    USERS ||--o{ ORDERS : "Places (1:N)"
    CATEGORIES ||--o{ PRODUCTS : "Contains (1:N)"
    PRODUCTS ||--o{ PRODUCT_DEGREES : "Has (1:N)"
    
    CARTS ||--o{ CART_ITEMS : "Contains (1:N)"
    PRODUCT_DEGREES ||--o{ CART_ITEMS : "Selected in (1:N)"
    
    ORDERS ||--|{ ORDER_ITEMS : "Includes (1:N)"
    PRODUCTS ||--o{ ORDER_ITEMS : "Snapshot from (1:N)"

    USERS {
        int user_id PK
        varchar username
        varchar password
        varchar email
        enum role
        datetime created_at
    }

    CATEGORIES {
        int category_id PK
        varchar category_name
    }

    PRODUCTS {
        int product_id PK
        varchar product_name
        varchar brand
        varchar color
        int pack_size
        decimal price
        text description
        varchar image_url
        int category_id FK
        datetime created_at
    }

    PRODUCT_DEGREES {
        int degree_id PK
        int product_id FK
        varchar degree
        int stock
    }

    CARTS {
        int cart_id PK
        int user_id FK "UNIQUE"
        datetime created_at
    }

    CART_ITEMS {
        int cart_item_id PK
        int cart_id FK "UK_1"
        int degree_id FK "UK_2"
        int quantity
    }

    ORDERS {
        int order_id PK
        int user_id FK
        decimal total_amount
        enum order_status
        datetime created_at
    }

    ORDER_ITEMS {
        int order_item_id PK
        int order_id FK
        int product_id FK
        varchar degree "History Snapshot"
        int quantity
        decimal price "History Snapshot"
    }
