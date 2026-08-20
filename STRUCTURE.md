# ShopFlat Project Structure

## Current State

The starter project uses a flat `src/` directory. Before changing any file locations, the complete inventory is:

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

This is **30 files** in one directory, mixing feature code, shared UI, shared hooks, utility functions, API services, and application bootstrapping. A new engineer would likely need approximately **2–4 hours** to find the cart checkout logic confidently because `CartSummary.jsx`, `CheckoutModal.jsx`, `cartService.js`, and `useCart.js` are separated from one another and are mixed with unrelated auth, product, order, and shared files.

## File Mapping

The following mapping is the planned destination for every file in the original flat `src/` directory. It is the move plan and is intentionally recorded before any file is relocated.

| Original file | Planned destination | Classification and rationale |
|---|---|---|
| `App.jsx` | `src/App.jsx` | Application composition and route-level shell; remains at the source root. |
| `main.jsx` | `src/main.jsx` | Application entry point; remains at the source root. |
| `index.css` | `src/index.css` | Global stylesheet; remains at the source root. |
| `LoginForm.jsx` | `src/features/auth/LoginForm.jsx` | Auth-specific UI. |
| `LogoutButton.jsx` | `src/features/auth/LogoutButton.jsx` | Auth-specific UI. |
| `loginService.js` | `src/features/auth/loginService.js` | Auth API and session operations. |
| `useLogin.js` | `src/features/auth/useLogin.js` | Auth-specific hook. |
| `ProductCard.jsx` | `src/features/products/ProductCard.jsx` | Product catalog UI. |
| `ProductList.jsx` | `src/features/products/ProductList.jsx` | Product catalog UI. |
| `productsService.js` | `src/features/products/productsService.js` | Product catalog API operations. |
| `useProducts.js` | `src/features/products/useProducts.js` | Product catalog hook. |
| `CartItem.jsx` | `src/features/cart/CartItem.jsx` | Cart-specific UI. |
| `CartSummary.jsx` | `src/features/cart/CartSummary.jsx` | Cart-specific UI and checkout entry point. |
| `CheckoutModal.jsx` | `src/features/cart/CheckoutModal.jsx` | Cart checkout UI. |
| `cartService.js` | `src/features/cart/cartService.js` | Cart persistence and checkout operations. |
| `useCart.js` | `src/features/cart/useCart.js` | Cart-specific hook. |
| `Dashboard.jsx` | `src/features/orders/Dashboard.jsx` | Order-history dashboard composition; it owns the orders overview screen. |
| `OrderCard.jsx` | `src/features/orders/OrderCard.jsx` | Order-history UI. |
| `OrdersList.jsx` | `src/features/orders/OrdersList.jsx` | Order-history UI and data loading. |
| `ordersService.js` | `src/features/orders/ordersService.js` | Order-history API operations. |
| `Button.jsx` | `src/components/Button.jsx` | Reusable UI component used by multiple features. |
| `EmptyState.jsx` | `src/components/EmptyState.jsx` | Reusable UI state component. |
| `ErrorMessage.jsx` | `src/components/ErrorMessage.jsx` | Reusable UI state component. |
| `Modal.jsx` | `src/components/Modal.jsx` | Reusable UI component used by checkout and potentially other flows. |
| `Navbar.jsx` | `src/components/Navbar.jsx` | Shared application navigation. |
| `Spinner.jsx` | `src/components/Spinner.jsx` | Reusable loading component. |
| `useDebounce.js` | `src/hooks/useDebounce.js` | Feature-neutral custom hook used by catalog search. |
| `formatCurrency.js` | `src/utils/formatCurrency.js` | Pure formatting utility. |
| `truncateText.js` | `src/utils/truncateText.js` | Pure text utility. |
| `apiClient.js` | `src/services/apiClient.js` | Shared API client used by feature services. |

## Target Structure

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

This target tree contains all **30 original files** and separates application features from reusable building blocks and infrastructure.

## Folder Rules

The `features/` folder contains code owned by a single product capability. Auth, cart, products, and orders each keep their components, hooks, and feature-specific services together. For example, `CheckoutModal.jsx` belongs in `features/cart/` because it completes a cart checkout, while `ProductCard.jsx` belongs in `features/products/` because it renders catalog data. If a file only makes sense in one feature, keep it inside that feature rather than promoting it to a shared folder.

The `components/` folder contains reusable UI used by multiple features or by the application shell. `Button.jsx`, `Modal.jsx`, `Spinner.jsx`, `EmptyState.jsx`, `ErrorMessage.jsx`, and `Navbar.jsx` are shared presentation pieces. If a component is used by only one feature, it should remain inside that feature instead of being placed here.

The `hooks/` folder contains custom React hooks that are not tied to a single business capability. `useDebounce.js` is shared behavior that can support search or other delayed input flows. Feature-specific hooks such as `useCart.js`, `useLogin.js`, and `useProducts.js` remain beside their owning feature.

The `utils/` folder contains pure, framework-independent functions with no React imports, side effects, or API calls. `formatCurrency.js` and `truncateText.js` are examples: they transform input into output and can be tested in isolation.

The `services/` folder contains shared infrastructure for external communication. `apiClient.js` is the common HTTP/mock client used by feature services. API operations that are specific to one capability remain in that capability's feature folder, such as `features/orders/ordersService.js`.

The `src/` root contains only application bootstrapping and global composition. `main.jsx` mounts React, `index.css` defines global styles, and `App.jsx` composes the feature screens and shared navigation. New business logic should not be added directly to the root.

## Decision Tree

For every new file, ask these questions in order:

1. Is it used by exactly one product feature? If yes, place it in `src/features/[feature-name]/`.
2. If not, is it a reusable UI component that renders JSX? If yes, place it in `src/components/`.
3. If not, is it a feature-neutral custom React hook? If yes, place it in `src/hooks/`.
4. If not, is it a pure function with no React dependency or side effects? If yes, place it in `src/utils/`; otherwise, place shared external-service infrastructure in `src/services/`.

## Adding a New Feature

1. Create `src/features/[feature-name]/` using the product capability's name.
2. Put components, feature-specific hooks, utilities, and API operations inside that feature folder.
3. Reuse shared UI from `src/components/`, feature-neutral hooks from `src/hooks/`, pure functions from `src/utils/`, and the shared client from `src/services/apiClient.js`.
4. Keep imports within the feature relative and update imports to shared folders with the correct relative path.
5. Compose the feature in `src/App.jsx` or the appropriate application shell component.
6. Run the build and inspect the feature's loading, error, empty, and success states before committing.
7. Update this document's target tree and folder rules when the new feature introduces a durable architectural convention.

## Before vs After

Before the refactor, all 30 files lived directly under `src/`, so a contributor had to scan unrelated auth, catalog, cart, order, and shared UI files to locate a workflow. The flat layout also made relative imports ambiguous because similarly named responsibilities were peers in the same directory.

After the refactor, ownership is visible from the path. Cart checkout logic can be found by opening `src/features/cart/` and locating `CheckoutModal.jsx` alongside `CartSummary.jsx`, `CartItem.jsx`, `cartService.js`, and `useCart.js`. Shared UI and infrastructure are clearly separated, making the codebase easier to onboard, navigate, and extend.
