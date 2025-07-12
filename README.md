# teacher-management-ui
// === Sample Teacher Type ===
// File: /types/teacher.d.ts
export interface Teacher {
  id: string;
  name: string;
  subject: string;
  email: string;
  salaryDue: number;
}

// === Sample JSON Data ===
// Could be replaced by API call later
const sampleTeachers: Teacher[] = [
  {
    id: "t1",
    name: "Arjun Rao",
    subject: "Mathematics",
    email: "arjun@school.edu",
    salaryDue: 5000,
  },
  {
    id: "t2",
    name: "Meera Iyer",
    subject: "English",
    email: "meera@school.edu",
    salaryDue: 0,
  },
];

// === Basic Payment Form Validation ===
// File: /utils/validation.ts
export function validatePaymentForm(amount: number, method: string): string | null {
  if (!amount || amount <= 0) return "Amount must be greater than zero";
  if (!method.trim()) return "Payment method is required";
  return null;
  }
  // === TeacherCard Component ===
// File: /components/TeacherCard.tsx
import React from "react";
import { Teacher } from "../types/teacher";

type Props = {
  teacher: Teacher;
  onPay: (teacher: Teacher) => void;
};

export const TeacherCard: React.FC<Props> = ({ teacher, onPay }) => {
  return (
    <div className="bg-white rounded-lg shadow p-4 space-y-2 hover:shadow-md transition-all">
      <h3 className="text-lg font-semibold">{teacher.name}</h3>
      <p className="text-sm text-gray-600">{teacher.subject}</p>
      <p className="text-sm text-gray-500">{teacher.email}</p>
      <p className="text-sm font-medium">
        Salary Due: ₹{teacher.salaryDue.toLocaleString()}
      </p>
      {teacher.salaryDue > 0 && (
        <button
          onClick={() => onPay(teacher)}
          className="mt-2 px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700 transition"
        >
          Pay Now
        </button>
      )}
    </div>
  );
};

// === PaymentForm Component ===
// File: /components/PaymentForm.tsx
import React, { useState } from "react";
import { validatePaymentForm } from "../utils/validation";

interface Props {
  teacherName: string;
  onSubmit: (amount: number, method: string) => void;
}

export const PaymentForm: React.FC<Props> = ({ teacherName, onSubmit }) => {
  const [amount, setAmount] = useState(0);
  const [method, setMethod] = useState("");
  const [error, setError] = useState<string | null>(null);

  const handleSubmit = () => {
    const validationError = validatePaymentForm(amount, method);
    if (validationError) return setError(validationError);
    setError(null);
    onSubmit(amount, method);
  };

  return (
    <div className="p-4 bg-gray-100 rounded-lg space-y-4">
      <h4 className="text-md font-semibold">Pay {teacherName}</h4>
      <input
        type="number"
        placeholder="Enter amount"
        value={amount}
        onChange={(e) => setAmount(Number(e.target.value))}
        className="w-full px-3 py-2 border rounded"
      />
      <input
        type="text"
        placeholder="Payment method (e.g., UPI, Bank Transfer)"
        value={method}
        onChange={(e) => setMethod(e.target.value)}
        className="w-full px-3 py-2 border rounded"
      />
      {error && <p className="text-red-500 text-sm">{error}</p>}
      <button
        onClick={handleSubmit}
        className="w-full bg-green-600 text-white px-3 py-2 rounded hover:bg-green-700"
      >
        Submit Payment
      </button>
    </div>
  );
};
