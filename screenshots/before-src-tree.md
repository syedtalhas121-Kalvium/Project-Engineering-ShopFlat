# ShopFlat Before Refactor

## `src/` — flat starter structure

```text
src/
├── App.jsx
├── Button.jsx
├── CartItem.jsx
├── CartSummary.jsx
├── CheckoutModal.jsx
├── Dashboard.jsx
├── EmptyState.jsx
├── ErrorMessage.jsx
├── LoginForm.jsx
├── LogoutButton.jsx
├── Modal.jsx
├── Navbar.jsx
├── OrderCard.jsx
├── OrdersList.jsx
├── ProductCard.jsx
├── ProductList.jsx
├── Spinner.jsx
├── apiClient.js
├── cartService.js
├── formatCurrency.js
├── index.css
├── loginService.js
├── main.jsx
├── ordersService.js
├── productsService.js
├── truncateText.js
├── useCart.js
├── useDebounce.js
├── useLogin.js
└── useProducts.js
```

**30 files in one folder:** feature code, shared UI, hooks, utilities, services, and app bootstrap are mixed together.
