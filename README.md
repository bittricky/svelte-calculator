# Svelte Calculator

A simple calculator app built with Svelte featuring a theme switcher and responsive design.

## Features

- Basic arithmetic operations (addition, subtraction, multiplication, division)
- Three color themes
- Responsive design
- DEL and RESET functionality
- Error handling for division by zero

## Prerequisites

- Node.js (version 14 or higher)
- npm (Node Package Manager)

## Setup

1. Clone the repository:

```bash
git clone [repository-url]
cd svelte-calculator
```

2. Install dependencies:

```bash
npm install
```

3. Start development server:

```bash
npm run dev
```

4. Open your browser and navigate to the URL shown in the terminal (usually `http://localhost:5173`)

## Build for Production

To create a production build:

```bash
npm run build
```

The built files will be in the `dist` directory.

## Project Structure

```
svelte-calculator/
├── src/
│   ├── App.svelte    # Main calculator component
│   └── main.js       # Application entry point
├── public/           # Static assets
├── index.html        # HTML template
├── package.json      # Project dependencies and scripts
├── vite.config.js    # Vite configuration
└── README.md         # Project documentation
```

## Technologies Used

- Svelte
- Vite
- CSS Custom Properties for theming
- League Spartan font

### Calculator Operations

- Numbers (0-9)
- Decimal point (.)
- Basic operations (+, -, ×, ÷)
- DEL: Removes the last entered digit
- RESET: Clears all entries
- EQUALS: Calculates the result
