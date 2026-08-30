# 04. Forms 📝

## Controlled form
```jsx
import { useState } from 'react';

export function Signup() {
  const [form, setForm] = useState({ email: '', password: '' });

  const onChange = e => setForm(f => ({ ...f, [e.target.name]: e.target.value }));

  return (
    <form>
      <input name="email" value={form.email} onChange={onChange} />
      <input name="password" type="password" value={form.password} onChange={onChange} />
    </form>
  );
}
```

## React Hook Form + Yup
```jsx
import { useForm } from 'react-hook-form';
import { yupResolver } from '@hookform/resolvers/yup';
import * as yup from 'yup';

const schema = yup.object({ email: yup.string().email().required() });

const { register, handleSubmit, formState: { errors } } = useForm({
  resolver: yupResolver(schema)
});
```

## File uploads
Use `FormData`, validate size/type client-side, scan server-side.

## Multi-step forms
Persist partial state and validate per step.

## When to use each
- React Hook Form: performance + minimal rerenders
- Formik: mature ecosystem/simple mental model

## When NOT to use
- Heavy form library for tiny 1-2 input forms
