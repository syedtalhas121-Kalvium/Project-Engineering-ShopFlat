# ShopFlat After Refactor

## `src/` — feature-based architecture

```text
src/
├── features/
│   ├── auth/
│   │   ├── LoginForm.jsx
│   │   ├── LogoutButton.jsx
│   │   ├── loginService.js
│   │   └── useLogin.js
│   ├── cart/
│   │   ├── CartItem.jsx
│   │   ├── CartSummary.jsx
│   │   ├── CheckoutModal.jsx
│   │   ├── cartService.js
│   │   └── useCart.js
│   ├── products/
│   │   ├── ProductCard.jsx
│   │   ├── ProductList.jsx
│   │   ├── productsService.js
│   │   └── useProducts.js
│   └── orders/
│       ├── Dashboard.jsx
│       ├── OrderCard.jsx
│       ├── OrdersList.jsx
│       └── ordersService.js
├── components/
│   ├── Button.jsx
│   ├── EmptyState.jsx
│   ├── ErrorMessage.jsx
│   ├── Modal.jsx
│   ├── Navbar.jsx
│   └── Spinner.jsx
├── hooks/
│   └── useDebounce.js
├── utils/
│   ├── formatCurrency.js
│   └── truncateText.js
├── services/
│   └── apiClient.js
├── App.jsx
├── index.css
└── main.jsx
```

**Ownership is visible from the path:** cart checkout logic is now together under `features/cart/`, while reusable UI, hooks, utilities, and service infrastructure have dedicated shared folders.
