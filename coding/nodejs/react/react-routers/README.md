# React Routers
Allows you to map urls to different page configurations.
https://reactrouter.com/en/main

React Router helps to use Client-side URL changes to map to react components.

Router v6 example:
```javascript
import {Navigate, Route, Routes} from 'react-router-dom';
import React from 'react';

export function MainView() {
  return (
    <Routes>
      <Route element={<WelcomeView />} path="/" />
      <Route element={<InventoryView />} path="/books" />
      <Route element={<InventoryView />} path="/books/:bookISBN" />
      <Route element={<Navigate replace to="/" />} path="/*" />
    </Routes>
  );
}
```
