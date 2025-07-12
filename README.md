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
  
