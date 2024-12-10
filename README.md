
# 📋 Custom Form with React Hook Form and Zod

This project demonstrates a customizable form component built with **React**, **React Hook Form**, and **Zod** for form validation. The form includes reusable components, validation rules, and error handling, providing a scalable solution for forms in React applications.

---

## ✨ Features

- 🔄 **Reusable Components**: Modular and reusable `InputForm` component.
- ✅ **Validation**: Form validation powered by **Zod** with a resolver from `@hookform/resolvers/zod`.
- 💻 **TypeScript Support**: Fully typed with **TypeScript** for better developer experience.
- ⚠️ **Error Handling**: Displays user-friendly error messages for each input field.
- 🎨 **Custom Design**: Easy-to-style components with CSS.

---

## 📂 Project Structure

```plaintext
src/
├── components/
│   ├── CustomForm/
│   │   └── CustomForm.tsx   // Main form component
│   ├── CustomInput/
│   │   └── CustomInput.tsx  // Reusable input component
│   └── CustomInput.css      // Styling for the input component
├── models/
│   └── index.ts             // Zod schema and form types
├── App.tsx                  // Main app entry
└── App.css                  // Global styles
```

---

## 🚀 Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-repository-name.git
   cd your-repository-name
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Start the development server**:
   ```bash
   npm start
   ```

---

## 🛠️ Usage

1. Define a schema in the `models/index.ts` file using **Zod** for form validation rules.
2. Add new input fields in the `CustomForm` component by utilizing the reusable `InputForm` component.
3. Customize styles in the `CustomInput.css` file.

---

## 🔧 Example Code

### **Zod Schema (Validation Rules)**

```typescript
import { z } from "zod";

export const schema = z.object({
  name: z.string().min(1, "Name is required"),
  email: z.string().email("Invalid email address"),
  password: z.string().min(6, "Password must be at least 6 characters long"),
  confirmPassword: z.string().refine((value, context) => value === context.parent.password, {
    message: "Passwords do not match",
  }),
});

export type FormValues = z.infer<typeof schema>;
```

### **Custom Form Component**

```typescript
import { useForm, SubmitHandler } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { FormValues, schema } from "../models";
import InputForm from "./CustomInput";

const CustomForm = () => {
  const { control, handleSubmit, formState: { errors } } = useForm<FormValues>({
    resolver: zodResolver(schema),
  });

  const onSubmit: SubmitHandler<FormValues> = (data) => {
    console.log(data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <InputForm name="name" control={control} label="Name" error={errors.name} />
      <InputForm name="email" control={control} label="Email" error={errors.email} />
      <InputForm name="password" control={control} label="Password" type="password" error={errors.password} />
      <InputForm name="confirmPassword" control={control} label="Confirm Password" type="password" error={errors.confirmPassword} />
      <button type="submit">Submit</button>
    </form>
  );
};

export default CustomForm;
```

---

## 🎨 Styling

You can customize the form styles in the `CustomInput.css` file. Below is an example of the default styling:

```css
.form-group {
  margin-bottom: 15px;
}

.form-control {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.form-control.is-invalid {
  border-color: red;
}

.error {
  color: red;
  font-size: 12px;
  margin-top: 5px;
}
```

---

## 🤝 Contributing

Feel free to open issues or submit pull requests if you have ideas for improvement or encounter any problems. Contributions are always welcome!

---

## 📄 License

This project is licensed under the **MIT License**. See the `LICENSE` file for more information.

---
