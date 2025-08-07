```markdown
# Detailed Implementation Plan: Gerenciamento de Finanças Pessoais

## Overview  
- Develop a Next.js personal finance management dashboard with features for controle de receitas e despesas, gerenciamento de orçamento, metas financeiras, categorização de transações, relatórios/gráficos, controle de poupança, lembretes de contas, and controle de cartões.  
- Use local storage for data persistence via a custom utility file.  
- Leverage Tailwind CSS and shadcn/ui best practices to achieve a modern, clean, and responsive interface without external icons or imagery.  
- Ensure robust error handling within all data operations and UI components.

## File Structure & New Components

### New Pages & Layout  
- **src/app/dashboard/layout.tsx**  
  - Create a two-column layout with a responsive sidebar and main content area.  
  - Wrap content in an error boundary to gracefully handle runtime errors.

- **src/app/dashboard/page.tsx**  
  - Serve as the main dashboard page, aggregating financial components (forms, lists, charts, etc.).  
  - Import and render key components from the finance directory.

### New Components under `src/components/finance`  
- **Sidebar.tsx**  
  - Build a modern vertical navigation menu with textual links (Dashboard, Transações, Orçamento, Metas, Poupança, Cartões, Lembretes, Relatórios).  
  - Use Next.js `Link` for client-side routing and apply clean typography and spacing.

- **IncomeExpenseForm.tsx**  
  - Develop a form with fields: tipo (receita/despesa), valor, descrição, data, categoria e, se necessário, cartão.  
  - Utilize react-hook-form for field validations and display error messages; on submission, save data via the finance storage utility.

- **TransactionList.tsx**  
  - Display a responsive table or list view of transactions retrieved from local storage.  
  - Implement error checks and display a friendly message when no data is available.

- **BudgetManager.tsx**  
  - Provide an interface to set or update the monthly budget and compare it against recorded expenses, employing progress bars or summaries.

- **FinancialGoals.tsx**  
  - Allow users to define metas financeiras (nome, valor alvo, prazo) and display progress visually.

- **CardControl.tsx**  
  - Manage credit card information by listing cards, control de cartões, and allow addition/edits with secure handling of sensitive data.

- **SavingsControl.tsx**  
  - Track and update savings with a display of deposit histories and current balances.

- **BillReminders.tsx**  
  - List and manage lembretes de contas, with due date alerts and options to add new reminders.

- **ReportsDashboard.tsx**  
  - Integrate the `recharts` library to render interactive and responsive charts (barra, pizza) summarizing income vs. expenses and category distributions.  
  - Include proper fallbacks to handle scenarios when data is missing.

### Utility File for Data Persistence  
- **src/lib/financeStorage.ts**  
  - Implement localStorage-based CRUD methods:  
    - `getTransactions` / `saveTransaction`  
    - `getBudget` / `saveBudget`  
    - `getGoals` / `saveGoal`  
    - `getCards` / `saveCard`  
    - `getSavings` / `saveSavings`  
    - `getBills` / `saveBill`  
  - Use try-catch blocks to gracefully handle errors and provide default fallbacks.

## Step-by-Step Implementation

1. **Dashboard Layout and Main Page**  
   - Create `src/app/dashboard/layout.tsx` to include a sidebar (imported from `Sidebar.tsx`) and content area; add an error boundary wrapper.  
   - Create `src/app/dashboard/page.tsx` to import and render components like IncomeExpenseForm, TransactionList, ReportsDashboard, etc.

2. **Sidebar Component**  
   - Develop `src/components/finance/Sidebar.tsx` with a modern, text-based navigation menu.  
   - Ensure that each navigation link uses Next.js `Link` and styled Tailwind classes for hover/focus effects.

3. **Income & Expense Management**  
   - Build `IncomeExpenseForm.tsx` with fields for type, value, description, date, and category.  
   - Integrate react-hook-form for data validation; on submit, call methods from `financeStorage.ts` to store the record, and handle errors using try-catch.

4. **Transactions List**  
   - Create `TransactionList.tsx` to retrieve and display transaction records from local storage.  
   - Render a table or list with error handling for empty or failed data retrieval.

5. **Budget, Goals, Cards, Savings & Bills Modules**  
   - Develop `BudgetManager.tsx` for monthly budget entry and summary visualization.  
   - Develop `FinancialGoals.tsx` to add and monitor financial goals.  
   - Build `CardControl.tsx` for managing credit card information securely.  
   - Build `SavingsControl.tsx` to update and display savings balances.  
   - Build `BillReminders.tsx` to list upcoming bills and set reminders with due date notifications.

6. **Reports Dashboard Integration**  
   - Develop `ReportsDashboard.tsx` using recharts to create interactive charts.  
   - Display visual summaries of income vs. expenses and transaction category distributions with responsive containers and error handling for no-data cases.

7. **Finance Storage Utility**  
   - Create `src/lib/financeStorage.ts` to encapsulate data persistence logic using localStorage.  
   - Implement robust error handling (try-catch) and default return values if data is missing or corrupted.

8. **UI/UX and Styling Enhancements**  
   - Apply Tailwind CSS classes for a modern and consistent design across forms, tables, and charts.  
   - Maintain proper layout, spacing, and typography; ensure responsiveness and a clear visual hierarchy.

9. **Testing & Error Handling**  
   - Test each component individually using the Next.js development server (using `npm run dev`) and check localStorage operations.  
   - Validate that error messages and fallbacks are displayed correctly when data operations fail.

## Summary  
- Created a Next.js dashboard under `src/app/dashboard` with a modern, responsive layout and sidebar navigation.  
- Developed dedicated finance components (IncomeExpenseForm, TransactionList, BudgetManager, etc.) to handle all key financial features.  
- Integrated a utility file (`src/lib/financeStorage.ts`) to manage localStorage with robust error handling.  
- Ensured a clean UI/UX with Tailwind CSS and styled components without external icons or images.  
- Included interactive charts using recharts in the ReportsDashboard component.  
- Followed best practices in error handling, component modularity, and responsive design.
