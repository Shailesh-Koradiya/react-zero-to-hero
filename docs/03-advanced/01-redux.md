# 01. Redux Toolkit 🧰

```jsx
import { configureStore, createAsyncThunk, createSlice } from '@reduxjs/toolkit';

export const fetchPosts = createAsyncThunk('posts/fetch', async () => {
  const res = await fetch('/api/posts');
  return res.json();
});

const postsSlice = createSlice({
  name: 'posts',
  initialState: { items: [], loading: false },
  reducers: {},
  extraReducers: builder => {
    builder
      .addCase(fetchPosts.pending, state => { state.loading = true; })
      .addCase(fetchPosts.fulfilled, (state, action) => {
        state.loading = false;
        state.items = action.payload;
      });
  }
});

export const store = configureStore({ reducer: { posts: postsSlice.reducer } });
```

## RTK Query
Use for API caching, tags invalidation, and reduced boilerplate.

## When to use Redux Toolkit
- Complex shared state with predictable transitions

## When NOT to use
- Tiny apps where local state/context is enough

> ⚠️ **Common mistake:** Storing derived/transient UI values globally.
