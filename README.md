# TodoReact - Modern Task Management Application

![React](https://img.shields.io/badge/React-19.2.0-61DAFB?style=for-the-badge&logo=react&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5.9.3-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-7.2.4-646CFF?style=for-the-badge&logo=vite&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4.1.17-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)
![DaisyUI](https://img.shields.io/badge/DaisyUI-5.5.5-5A0EF8?style=for-the-badge&logo=daisyui&logoColor=white)

> A sleek, modern, and feature-rich todo application built with cutting-edge web technologies. Manage your tasks with style using priority levels, smart filtering, and batch operations—all in a beautiful dark-themed interface!

---

## Table of Contents

- [Features](#features)
- [Screenshots](#screenshots)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [How It Works](#how-it-works)
- [Development](#development)
- [Build & Deployment](#build--deployment)
- [Contributing](#contributing)
- [License](#license)

---

## Features

### Core Functionality

- **Add Tasks with Priorities** - Create todos and assign priority levels (Urgent, Medium, Low)
- **Smart Filtering System** - View all tasks or filter by priority level with live counters
- **Individual Task Deletion** - Remove single tasks with a click
- **Batch Operations** - Select multiple tasks and delete them all at once
- **Local Persistence** - All your tasks are automatically saved to your browser's localStorage
- **Responsive Design** - Works beautifully on desktop, tablet, and mobile devices

### Priority Management

Each task can be assigned one of three priority levels:

- **Urgente** (Urgent) - Red badge for critical tasks
- **Moyenne** (Medium) - Orange badge for standard tasks
- **Basse** (Low) - Green badge for less important tasks

### User Experience

- **Dark Theme** - Easy on the eyes with DaisyUI's "night" theme
- **French Interface** - All labels and messages in French
- **Empty State Handling** - Beautiful construction icon when no tasks match your filter
- **Real-time Updates** - Instant feedback on all operations
- **Input Validation** - Prevents adding empty tasks
- **Smart Defaults** - Priority resets to "Moyenne" after adding a task

---

## Screenshots

### Main Interface
The application features a clean, centered layout with:
- Input field for task text
- Priority selector dropdown
- Filter buttons with live counters
- Batch delete functionality
- Task list with priority badges

### Empty State
When no tasks match your filter, you'll see a friendly construction icon with a message: "Aucunes tâches pour ce filtre" (No tasks for this filter).

---

## Tech Stack

### Frontend Framework
- **React 19.2.0** - The latest version of React with improved performance and new features
- **TypeScript 5.9.3** - Strict type safety for robust code
- **React DOM 19.2.0** - React rendering library

### Build Tools
- **Vite 7.2.4** - Lightning-fast build tool and dev server with Hot Module Replacement (HMR)
- **@vitejs/plugin-react 5.1.1** - Official React plugin for Vite with Fast Refresh support

### Styling
- **Tailwind CSS 4.1.17** - Utility-first CSS framework for rapid UI development
- **@tailwindcss/vite 4.1.17** - Tailwind CSS Vite integration
- **DaisyUI 5.5.5** - Beautiful component library built on top of Tailwind CSS
- **Lucide React 0.555.0** - Gorgeous icon library (used for Trash and Construction icons)

### Code Quality
- **ESLint 9.39.1** - JavaScript/TypeScript linting
- **typescript-eslint 8.46.4** - TypeScript-specific linting rules
- **eslint-plugin-react-hooks 7.0.1** - Enforces React Hooks rules
- **eslint-plugin-react-refresh 0.4.24** - Ensures Fast Refresh compatibility

---

## Getting Started

### Prerequisites

- Node.js (version 16 or higher recommended)
- npm or yarn package manager

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/ValentinColombat/Todo-React.git
   cd TodoReact
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start the development server**
   ```bash
   npm run dev
   ```

4. **Open your browser**

   Navigate to `http://localhost:5173` (default Vite port)

That's it! You're ready to start managing your tasks.

---

## Project Structure

```
TodoReact/
├── src/
│   ├── App.tsx           # Main application component (state management, logic)
│   ├── TodoItem.tsx      # Individual todo item component (presentational)
│   ├── main.tsx          # React entry point
│   └── index.css         # Global styles (Tailwind imports)
├── public/
│   └── vite.svg          # Vite logo/favicon
├── index.html            # HTML entry point with dark theme configuration
├── vite.config.ts        # Vite build configuration
├── tsconfig.json         # TypeScript configuration reference
├── tsconfig.app.json     # App-specific TypeScript settings
├── tsconfig.node.json    # Node environment TypeScript settings
├── eslint.config.js      # ESLint configuration
├── package.json          # Dependencies and scripts
└── README.md             # This file!
```

### File Descriptions

#### [src/App.tsx](src/App.tsx)
The brain of the application! This component handles:
- **State Management**: Manages todos, input, priority, filters, and selections
- **localStorage Integration**: Automatically saves and loads todos
- **CRUD Operations**: Create, Read, and Delete functionality
- **Filtering Logic**: Computes filtered todos based on selected priority
- **Counter Calculations**: Counts todos by priority for filter buttons
- **UI Layout**: Renders input area, filters, and todo list

#### [src/TodoItem.tsx](src/TodoItem.tsx)
A presentational component for individual tasks:
- Displays task text and priority badge
- Shows checkbox for batch selection
- Provides delete button with trash icon
- Color-coded priority badges (red/orange/green)
- Receives props: `todo`, `onDelete`, `isSelected`, `onToggleSelect`

#### [src/main.tsx](src/main.tsx)
Application entry point:
- Initializes React with StrictMode
- Mounts the App component to the DOM

#### [src/index.css](src/index.css)
Global styles configuration:
```css
@import "tailwindcss";
@plugin "daisyui" {
  themes: night
};
```

---

## How It Works

### Data Model

The application uses TypeScript for type safety with the following models:

```typescript
type Priority = "Urgente" | "Moyenne" | "Basse"

type Todo = {
  id: number;
  text: string;
  priority: Priority;
}
```

### State Management

The app uses React's `useState` hooks to manage:

| State | Type | Purpose |
|-------|------|---------|
| `todos` | `Todo[]` | Array of all todo items |
| `input` | `string` | Current input field value |
| `priority` | `Priority` | Currently selected priority |
| `filter` | `Priority \| "Tous"` | Active filter |
| `selectedTodos` | `Set<number>` | Set of selected todo IDs for batch operations |

### Key Functions

#### Adding a Todo ([App.tsx:26-42](src/App.tsx#L26-L42))
```typescript
function addTodo() {
  if (input.trim() === "") return; // Validation

  const newTodo: Todo = {
    id: Date.now(),              // Unique timestamp ID
    text: input.trim(),
    priority: priority
  }

  setTodos([newTodo, ...todos]); // Prepend to array
  setInput("");                   // Clear input
  setPriority("Moyenne");        // Reset priority
}
```

#### Deleting a Single Todo ([App.tsx:57-60](src/App.tsx#L57-L60))
```typescript
function deleteTodo(id: number) {
  const newTodos = todos.filter((todo) => todo.id !== id);
  setTodos(newTodos);
}
```

#### Batch Selection Toggle ([App.tsx:64-72](src/App.tsx#L64-L72))
```typescript
function toggleSelectTodo(id: number) {
  const newSelected = new Set(selectedTodos);
  if (newSelected.has(id)) {
    newSelected.delete(id);
  } else {
    newSelected.add(id);
  }
  setSelectedTodos(newSelected);
}
```

#### Batch Deletion ([App.tsx:74-83](src/App.tsx#L74-L83))
```typescript
function finishSelected() {
  const newTodos = todos.filter((todo) => !selectedTodos.has(todo.id));
  setTodos(newTodos);
  setSelectedTodos(new Set()); // Clear selection
}
```

### Data Persistence

The app uses `useEffect` to automatically sync todos with localStorage:

```typescript
useEffect(() => {
  localStorage.setItem("todos", JSON.stringify(todos));
}, [todos]);
```

On initial load, it retrieves saved todos:

```typescript
const savedTodos = localStorage.getItem("todos");
const initialTodos = savedTodos ? JSON.parse(savedTodos) : [];
const [todos, setTodos] = useState<Todo[]>(initialTodos);
```

### Filtering System ([App.tsx:44-55](src/App.tsx#L44-L55))

The app computes filtered todos and counters in real-time:

```typescript
// Filter todos based on selected filter
let filteredTodos: Todo[] = [];
if (filter === "Tous") {
  filteredTodos = todos;
} else {
  filteredTodos = todos.filter((todo) => todo.priority === filter);
}

// Calculate counters for each priority
const urgentCount = todos.filter((t) => t.priority === "Urgente").length;
const mediumCount = todos.filter((t) => t.priority === "Moyenne").length;
const lowCount = todos.filter((t) => t.priority === "Basse").length;
const totalCount = todos.length;
```

---

## Development

### Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start development server with HMR at `http://localhost:5173` |
| `npm run build` | Type-check with TypeScript and build for production |
| `npm run lint` | Run ESLint to check code quality |
| `npm run preview` | Preview production build locally |

### Development Workflow

1. **Start the dev server**: `npm run dev`
2. **Make your changes** - Vite's HMR will instantly reflect changes
3. **Check for errors**: TypeScript will show type errors in your IDE
4. **Lint your code**: `npm run lint` before committing
5. **Build for production**: `npm run build` to verify everything compiles

### Code Quality Tools

#### TypeScript Configuration
- **Strict Mode**: Enabled for maximum type safety
- **Target**: ES2022 for modern JavaScript features
- **JSX**: react-jsx for optimal React performance
- **Checks**: Unused locals and parameters are flagged

#### ESLint Rules
- JavaScript recommended rules
- TypeScript recommended type-checking
- React Hooks rules enforcement
- React Refresh compatibility checks
- Browser globals support
- ECMAScript 2020 target

### Hot Module Replacement (HMR)

Vite provides blazing-fast HMR:
- Changes to React components refresh instantly
- State is preserved where possible
- No full page reload needed
- Sub-second update times

---

## Build & Deployment

### Production Build

Create an optimized production build:

```bash
npm run build
```

This will:
1. Run TypeScript compiler (`tsc -b`) to check for type errors
2. Build optimized bundles with Vite
3. Output production-ready files to `dist/` directory

### Build Output

The `dist/` folder will contain:
- Minified JavaScript bundles
- Optimized CSS
- HTML entry point
- Static assets (images, icons)

### Preview Production Build

Test the production build locally:

```bash
npm run preview
```

### Deployment Options

You can deploy this app to various platforms:

#### Vercel
```bash
npm install -g vercel
vercel
```

#### Netlify
```bash
npm install -g netlify-cli
netlify deploy
```

#### GitHub Pages
1. Build the project: `npm run build`
2. Push the `dist/` folder to a `gh-pages` branch
3. Enable GitHub Pages in repository settings

#### Docker
Create a `Dockerfile`:
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
EXPOSE 5173
CMD ["npm", "run", "preview"]
```

---

## Contributing

We welcome contributions! Here's how you can help:

### Reporting Bugs
- Open an issue describing the bug
- Include steps to reproduce
- Mention your browser and OS

### Suggesting Features
- Open an issue with your feature request
- Explain the use case and benefits
- Discuss implementation ideas

### Pull Requests
1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Make your changes
4. Run tests and linting: `npm run lint`
5. Commit your changes: `git commit -m 'Add amazing feature'`
6. Push to the branch: `git push origin feature/amazing-feature`
7. Open a Pull Request

### Code Style
- Follow the existing code style
- Use TypeScript with proper typing
- Add comments for complex logic
- Keep functions small and focused
- Use meaningful variable names

---

## Architecture Highlights

### Component Architecture
- **Smart/Dumb Components**: App.tsx is the smart component, TodoItem.tsx is presentational
- **Props Down, Events Up**: TodoItem receives props and emits events via callbacks
- **Single Responsibility**: Each component has a clear, focused purpose

### State Management Philosophy
- **Minimal State**: Only essential state is tracked
- **Derived Values**: Counters and filtered lists are computed, not stored
- **Immutable Updates**: Always create new arrays/objects instead of mutating

### Performance Considerations
- **Set for Selection**: Using JavaScript Set for O(1) lookup of selected todos
- **Key Props**: Proper keys on list items for efficient React reconciliation
- **No Unnecessary Re-renders**: Components only re-render when their props/state change

### Type Safety
- **Strict TypeScript**: Full type coverage with strict mode enabled
- **Type Definitions**: Clear interfaces for all data structures
- **Type Guards**: Runtime validation where needed (e.g., priority casting)

---

## Future Enhancements

Some ideas for future development:

- [ ] **Drag & Drop**: Reorder tasks by dragging
- [ ] **Due Dates**: Add deadlines to tasks
- [ ] **Categories/Tags**: Organize tasks beyond priorities
- [ ] **Search**: Filter tasks by text search
- [ ] **Dark/Light Toggle**: User-selectable theme
- [ ] **Task Completion**: Mark tasks as done without deleting
- [ ] **Edit Tasks**: Modify existing task text and priority
- [ ] **Export/Import**: Save/load todos as JSON
- [ ] **Multi-language**: Support for English, Spanish, etc.
- [ ] **Animations**: Smooth transitions for add/delete operations
- [ ] **Cloud Sync**: Optional backend for cross-device sync
- [ ] **Keyboard Shortcuts**: Power user features

---

## Author

**Valentin Colombat**

---

## License

This project is private and not currently licensed for public use.

---

## Acknowledgments

Built with love using:
- [React](https://react.dev/) - The library for web and native user interfaces
- [TypeScript](https://www.typescriptlang.org/) - JavaScript with syntax for types
- [Vite](https://vitejs.dev/) - Next generation frontend tooling
- [Tailwind CSS](https://tailwindcss.com/) - Rapidly build modern websites
- [DaisyUI](https://daisyui.com/) - The most popular component library for Tailwind CSS
- [Lucide](https://lucide.dev/) - Beautiful & consistent icons

---

**Happy Task Managing!** If you have any questions or suggestions, feel free to open an issue or reach out.

Made with TypeScript, React, and lots of coffee.
