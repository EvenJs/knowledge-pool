### Q: Users complain the dashboard takes several seconds to load data after login.

> Explain implementing loading states and skeleton screens while asynchronously fetching data. Use Promise.all to parallelize multiple API calls.

```javascript
useEffect(() => {
  Promise.all([fetchUser(), fetchOrders()]).finally(() => setLoading(false));
}, []);
```

### Q: Preventing Unnecessary Re-renders

> Mention React.memo, useMemo, and useCallback to avoid unnecessary re-renders.

```javascript
const memoizedList = useMemo(() => heavyList.map(...), [heavyList]);
```

### Q: Responsive UI Across Devices

> Use CSS Flexbox/Grid, media queries, or responsive libraries like TailwindCSS or Bootstrap.

```css
@media (max-width: 768px) {
  .container {
    flex-direction: column;
  }
}
```

> Highlight testing on Chrome DevTools and responsive design best practices.

### Q: Handling API Errors Gracefully

> Add try–catch and user-friendly error UI. Centralize handling with Axios interceptors or error boundaries.

```javascript
try {
  await axios.get("/api/data");
} catch {
  setError("Failed to load data");
}
```
