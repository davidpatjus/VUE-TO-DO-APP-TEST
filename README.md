# Vue Todo App

This is a simple Todo application built with Vue.js 3 and Vuetify. It allows users to manage tasks by adding, editing, completing, and deleting them.

## Features

- List tasks
- Add new tasks
- Edit existing tasks
- Mark tasks as completed
- Delete tasks
- Basic form validation

## Project Setup

### Prerequisites

- Node.js (v14 or later recommended)
- npm or yarn

### Installation

1. Clone the repository:
   \`\`\`
   git clone https://github.com/your-username/vue-todo-app.git
   cd vue-todo-app
   \`\`\`

2. Install dependencies:
   \`\`\`
   npm install
   # or
   yarn install
   \`\`\`

3. Run the development server:
   \`\`\`
   npm run dev
   # or
   yarn dev
   \`\`\`

4. Open your browser and visit \`http://localhost:5173\` (or the URL provided in the terminal).

## Project Structure

- \`src/App.vue\`: Main application component
- \`src/components/TaskForm.vue\`: Reusable component for adding tasks
- \`src/main.js\`: Entry point of the application

## Implementation Details

- The application uses Vue 3's Composition API for better organization and reusability of code.
- Vuetify is used for UI components and styling.
- State is managed locally within the App component using \`ref\` from Vue's reactivity API.
- The TaskForm component demonstrates component communication using props and events.
- Basic form validation is implemented to prevent empty tasks from being added.