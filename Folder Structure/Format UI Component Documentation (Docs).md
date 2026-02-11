## 🔹 Component: Button

Location:

`packages/ui/components/atoms/Button.tsx`

---

### Props

`interface ButtonProps {   variant: 'primary' | 'secondary' | 'danger'   size?: 'sm' | 'md' | 'lg'   loading?: boolean   disabled?: boolean   onClick?: () => void   children: React.ReactNode }`

---

### Behavior

- Jika `loading=true`, button disabled otomatis
    
- Variant menentukan warna berdasarkan theme
    
- Tidak mengatur margin eksternal (layout responsibility)
    

---

### Usage

```html
<Button variant="primary" size="md">   Submit </Button>
```