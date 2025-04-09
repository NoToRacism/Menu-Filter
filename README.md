# React Menu Project

A React application that displays a restaurant menu from a local data source and allows users to filter the items by category using dynamically generated buttons.

**[Live Demo]()**

## Features

- Displays menu items from a local data source (`data.js`) including image, title, price, and description.
- **Dynamic Filtering:** Allows users to filter menu items by category.
- Generates category filter buttons automatically based on the data.
- Includes an 'All' button to reset the filter and show all items.
- Built entirely with functional components and React Hooks (`useState`).
- Demonstrates state management, props drilling, event handling, and conditional rendering in React.

## Tech Stack

- [React](https://reactjs.org/)

## Project Structure

/public└── images/ # Contains menu item images (e.g., item-1.jpeg)/src├── App.jsx # Main component, state management, filtering logic├── Categories.jsx # Renders category filter buttons├── Menu.jsx # Renders the list of MenuItem components├── MenuItem.jsx # Renders a single menu item card├── Title.jsx # Reusable title component├── data.js # Menu data source (array of objects)├── index.css # Global styles / Component styles└── index.js # Application entry point

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

- Node.js (v14 or later recommended)
- npm (usually comes with Node.js) or yarn

### Installation

1.  **Clone the repository:**

    ```bash
    git clone <your-repository-url>
    ```

    _(Replace `<your-repository-url>` with your actual repository link)_

2.  **Navigate to the project directory:**

    ```bash
    cd <project-directory-name>
    ```

3.  **Install dependencies:**
    Using npm:
    ```bash
    npm install
    ```
    or using yarn:
    ```bash
    yarn install
    ```
4.  **Set up images:**
    - Create a folder named `images` inside the `public` directory (`public/images/`).
    - Place your menu item images (e.g., `item-1.jpeg`, `item-2.jpeg`, etc.) inside this `public/images/` folder. Ensure the filenames match the `img` paths specified in your `src/data.js` file.

## Available Scripts

In the project directory, you can run:

### `npm start` or `yarn start`

Runs the app in development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.
The page will reload if you make edits.

### `npm test` or `yarn test`

Launches the test runner in interactive watch mode.

### `npm run build` or `yarn build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

## How It Works

1.  **Data (`data.js`):** The menu items (with `id`, `title`, `category`, `price`, `img`, `desc`) are stored in an array exported from `src/data.js`.
2.  **State Management (`App.jsx`):**
    - The `App` component imports the menu `data`.
    - It calculates all unique categories from the data and creates an `allCategories` array (including 'all').
    - It uses `useState` to manage two pieces of state:
      - `menuItems`: An array holding the items currently displayed on the screen (initially all items).
      - `categories`: An array holding the category names for the filter buttons.
    - The `filterItems` function is defined here. It takes a `category` name, filters the original `data` based on that category (or resets to all data if 'all' is clicked), and updates the `menuItems` state using `setMenuItems`.
3.  **Component Rendering & Props (`App.jsx` -> `Categories.jsx` / `Menu.jsx`):**
    - `App` renders the `Title`, `Categories`, and `Menu` components.
    - It passes the `categories` state and the `filterItems` function down as props to the `Categories` component.
    - It passes the `menuItems` state down as a prop (`itemsToRender`) to the `Menu` component.
4.  **Filter Buttons (`Categories.jsx`):**
    - Receives the list of `categoriesAvailable` and the `onCategoryClick` function (which is `filterItems` from `App`).
    - Maps over the `categoriesAvailable` array to render a button for each category.
    - Each button's `onClick` handler calls the `onCategoryClick` function, passing up the specific category name that was clicked.
5.  **Display Logic (`Menu.jsx` -> `MenuItem.jsx`):**
    - `Menu` receives the filtered list of `itemsToRender`.
    - It maps over this array. For each `menuItemObject`, it renders a `MenuItem` component.
    - It uses the spread operator (`{...menuItemObject}`) to pass all properties of the item down as individual props to `MenuItem`.
    - `MenuItem` receives props like `img`, `title`, `price`, `desc` and displays the information for a single menu item card.
